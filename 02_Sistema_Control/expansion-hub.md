# Expansion Hub - Expandiendo las Capacidades del Robot

## Introducción

El **REV Expansion Hub (REV-31-1153)** es un módulo adicional que se conecta al Control Hub para proporcionar puertos extra de motores, servos y sensores. Es esencial para robots complejos que requieren más de 4 motores o 6 servos.

## Especificaciones Técnicas

### Puertos y Conectividad

El Expansion Hub tiene las mismas capacidades de I/O que el Control Hub:

#### Puertos de Motor
- **Cantidad**: 4 puertos DC motor
- **Corriente**: 10A continuo, 15A pico por motor
- **Encoder Support**: Sí, integrado

#### Puertos de Servo
- **Cantidad**: 6 puertos PWM
- **Voltaje**: 5V
- **Corriente Total**: 6A compartidos

#### Puertos de Sensor

**I2C**: 4 buses independientes
**Digital I/O**: 8 puertos
**Analog**: 4 puertos

### Diferencias con el Control Hub

| Característica | Control Hub | Expansion Hub |
|----------------|-------------|---------------|
| Procesador Android | ✓ | ✗ |
| Wi-Fi Integrado | ✓ | ✗ |
| IMU Integrada | ✓ | ✗ (puede conectar externa) |
| Puertos de Motor | 4 | 4 |
| Puertos de Servo | 6 | 6 |
| Conexión Principal | Wi-Fi/USB | RS485 al Control Hub |
| Alimentación | Batería directa (XT30) | Batería directa (XT30) |

## Conexión al Control Hub

### Cable RS485

El Expansion Hub se conecta al Control Hub mediante un cable RS485 especializado.

#### Especificaciones del Cable

- **Tipo**: JST PH 4-pin
- **Longitudes Disponibles**: 150mm, 300mm, 600mm
- **Pines**: GND, VCC, A, B (comunicación diferencial)

#### Conexión Física

1. Localiza el puerto "RS485" en el Control Hub
2. Conecta un extremo del cable RS485
3. Conecta el otro extremo al puerto correspondiente del Expansion Hub
4. Asegura las conexiones con amarres de cable

#### Diagrama de Conexión

```
[Batería 1] -----> [Control Hub] <--RS485--> [Expansion Hub] <----- [Batería 2]
                        |                             |
                        |                             |
                    Motores 0-3                   Motores 0-3
                    Servos 0-5                    Servos 0-5
```

**Nota**: Cada hub puede tener su propia batería o compartir una mediante distribución apropiada.

## Configuración de Hardware

### Escanear el Expansion Hub

1. En Driver Station o interfaz web, ve a "Configure Robot"
2. Crea nueva configuración o edita existente
3. El sistema detectará automáticamente el Expansion Hub conectado vía RS485
4. Aparecerá como "Expansion Hub 2" (el Control Hub es implícitamente "Hub 1")

### Mapear Dispositivos

Los dispositivos en el Expansion Hub se nombran de manera similar al Control Hub, pero es recomendable usar nombres que indiquen su ubicación:

**Ejemplo de Convención de Nombres:**

```
Control Hub:
  - Motor 0: frontLeftDrive
  - Motor 1: frontRightDrive
  - Motor 2: backLeftDrive
  - Motor 3: backRightDrive

Expansion Hub:
  - Motor 0: armLiftMotor
  - Motor 1: intakeMotor
  - Motor 2: hangMotor
  - Motor 3: (disponible)
  - Servo 0: clawServo
  - Servo 1: armRotateServo
```

### Configuración en Código

```java
// Motores del Control Hub (drivetrain)
DcMotor frontLeft = hardwareMap.get(DcMotor.class, "frontLeftDrive");
DcMotor frontRight = hardwareMap.get(DcMotor.class, "frontRightDrive");

// Motores del Expansion Hub (mecanismos)
DcMotor armLift = hardwareMap.get(DcMotor.class, "armLiftMotor");
DcMotor intake = hardwareMap.get(DcMotor.class, "intakeMotor");

// Servos del Expansion Hub
Servo claw = hardwareMap.get(Servo.class, "clawServo");
```

El SDK de FTC maneja automáticamente la comunicación con el Expansion Hub apropiado basándose en la configuración.

## Alimentación del Expansion Hub

### Opciones de Alimentación

#### Opción 1: Batería Separada (Recomendado)

**Ventajas**:
- Mayor corriente total disponible
- Aislamiento de cargas pesadas
- Redundancia en caso de fallo de batería

**Conexión**:
```
Batería 1 (12V) -> Control Hub -> Drivetrain (4 motores)
Batería 2 (12V) -> Expansion Hub -> Mecanismos (4 motores)
```

**Implementación**:
1. Conecta una batería al XT30 del Control Hub
2. Conecta segunda batería al XT30 del Expansion Hub
3. Asegura ambas baterías al chasis
4. Usa interruptores separados o un interruptor dual

#### Opción 2: Batería Compartida con Power Distribution

**Ventajas**:
- Una sola batería
- Menos peso
- Menos costo

**Desventajas**:
- Toda la corriente viene de una fuente
- Riesgo de caída de voltaje bajo carga pesada

**Implementación**:
1. Usa un Anderson PowerPole Y-cable o power distribution board
2. Conecta batería al distribuidor
3. Distribuye a Control Hub y Expansion Hub

## Consideraciones de Latencia

### Comunicación RS485

La comunicación entre Control Hub y Expansion Hub introduce latencia mínima:

- **Latencia Típica**: 1-2 ms
- **Velocidad de Datos**: 115200 baud
- **Actualización de Comandos**: Cada ciclo de OpMode (~50-100 Hz)

### Mejores Prácticas

1. **Usa Control Hub para sistemas críticos**:
   - Drivetrain en Control Hub (menor latencia)
   - Mecanismos auxiliares en Expansion Hub

2. **Evita operaciones sensibles a tiempo en Expansion Hub**:
   - Navegación autónoma precisa
   - Control PID de alta frecuencia

3. **Es aceptable para**:
   - Mecanismos de intake/outtake
   - Lifts y brazos
   - Servos de garra

## Uso Avanzado

### Múltiples Expansion Hubs

**Nota**: FTC permite hasta 1 Expansion Hub adicional (total: 1 Control Hub + 1 Expansion Hub).

Si requieres más puertos, considera:
- **Multiplexores I2C**: Para más sensores I2C
- **Servo Controllers externos**: Para más servos (verifica reglas)
- **Motor Y-cables**: Para motores que deben moverse síncronamente

### Monitoreo de Estado

```java
// Verificar conexión del Expansion Hub
public void checkExpansionHubConnection() {
    // El SDK lanza excepciones si hay problemas de comunicación
    try {
        double voltage = hardwareMap.voltageSensor.get("Expansion Hub 2").getVoltage();
        telemetry.addData("Expansion Hub Voltage", "%.2f V", voltage);
    } catch (Exception e) {
        telemetry.addData("Expansion Hub", "ERROR: No conectado");
    }
    telemetry.update();
}
```

### Sincronización de Comandos

Para asegurar que los comandos al Control Hub y Expansion Hub se ejecuten síncronamente:

```java
// Los comandos se envían en el mismo ciclo de OpMode
frontLeft.setPower(leftPower);    // Control Hub
frontRight.setPower(rightPower);  // Control Hub
armLift.setPower(armPower);       // Expansion Hub
intake.setPower(intakePower);     // Expansion Hub

// El SDK maneja el envío sincronizado internamente
```

## Troubleshooting

### Expansion Hub No Detectado

**Síntomas**: No aparece en la configuración de hardware

**Soluciones**:
1. Verifica cable RS485 conectado firmemente en ambos extremos
2. Prueba con cable RS485 diferente (puede estar dañado)
3. Verifica que el Expansion Hub esté encendido (LED verde)
4. Reinicia el Control Hub
5. Verifica que el firmware del Expansion Hub esté actualizado

### Motores del Expansion Hub No Responden

**Síntomas**: Motores del Control Hub funcionan, pero los del Expansion Hub no

**Diagnóstico**:
1. Verifica voltaje de la batería conectada al Expansion Hub
2. Usa "Self Inspect" para verificar comunicación RS485
3. Verifica que los nombres en el código coincidan con la configuración
4. Prueba los motores en los puertos del Control Hub (descartar motor defectuoso)

**Código de Prueba**:
```java
@TeleOp(name="Test Expansion Hub")
public class TestExpansionHub extends LinearOpMode {
    @Override
    public void runOpMode() {
        DcMotor motor = hardwareMap.get(DcMotor.class, "armLiftMotor");

        waitForStart();

        while (opModeIsActive()) {
            if (gamepad1.a) {
                motor.setPower(0.5);
                telemetry.addData("Expansion Motor", "Running");
            } else {
                motor.setPower(0);
                telemetry.addData("Expansion Motor", "Stopped");
            }

            // Mostrar voltaje de ambos hubs
            for (VoltageSensor sensor : hardwareMap.voltageSensor) {
                telemetry.addData(sensor.getDeviceName(), "%.2f V", sensor.getVoltage());
            }

            telemetry.update();
        }
    }
}
```

### Latencia Perceptible

**Síntomas**: Retraso notable en respuesta de motores/servos del Expansion Hub

**Soluciones**:
1. Verifica que el cable RS485 no esté dañado
2. Acorta el cable RS485 si es muy largo (máx. 600mm recomendado)
3. Aleja el cable RS485 de fuentes de interferencia electromagnética
4. Mueve componentes críticos al Control Hub
5. Reduce la carga computacional del OpMode

### Reinicios Inesperados del Expansion Hub

**Síntomas**: Expansion Hub se reinicia durante operación

**Causas Comunes**:
1. Caída de voltaje de batería bajo carga
2. Corriente total excede capacidad de la batería
3. Conexión floja de batería
4. Cable RS485 proporciona energía insuficiente (no debe usarse para energía principal)

**Soluciones**:
1. Usa batería completamente cargada (>12V)
2. Usa batería de mayor capacidad (verifica reglas)
3. Asegura conexión XT30 con velcro o soporte mecánico
4. Distribuye carga entre dos baterías
5. Reduce corriente pico (evita acelerar todos los motores simultáneamente)

## Mejores Prácticas

### Organización de Hardware

1. **Drivetrain en Control Hub**:
   - Menor latencia
   - Mayor confiabilidad
   - Acceso directo a IMU integrada

2. **Mecanismos en Expansion Hub**:
   - Lifts, brazos
   - Intakes, outtakes
   - Sistemas auxiliares

3. **Sensores Críticos en Control Hub**:
   - Sensores de navegación (IMU, odometría)
   - Cámaras (USB al Control Hub)

4. **Sensores No Críticos en Expansion Hub**:
   - Sensores de color para detección de elementos
   - Limit switches de mecanismos

### Gestión de Cables

- **Etiqueta** todos los cables (Control Hub vs Expansion Hub)
- **Usa colores** diferentes para diferenciar (opcional)
- **Ruta clara** del cable RS485, evitando áreas de movimiento
- **Protección**: Usa canaletas para el cable RS485

### Redundancia

- Lleva cables RS485 de repuesto a competencias
- Configura el robot para funcionar con solo el Control Hub en emergencia
- Documenta qué componentes están en cada hub

## Actualización de Firmware

### Proceso

El firmware del Expansion Hub se actualiza desde la interfaz del Control Hub:

1. Conecta al Wi-Fi del Control Hub
2. Navega a `192.168.43.1:8080`
3. Manage → Update Expansion Hub Firmware
4. Selecciona el archivo `.bin` del firmware
5. **No interrumpas** el proceso de actualización
6. El Expansion Hub se reiniciará automáticamente

### Verificación

```java
// Verificar versión de firmware en código
telemetry.addData("Expansion Hub FW",
    hardwareMap.get(LynxModule.class, "Expansion Hub 2").getFirmwareVersion());
telemetry.update();
```

## Próximos Pasos

- [Driver Station](./driver-station.md) - Configurar interfaz de control
- [Comunicaciones](./comunicaciones.md) - Optimizar Wi-Fi y RS485
- [Sistema Eléctrico](../04_Sistema_Electrico/alimentacion.md) - Gestión de múltiples fuentes de energía

---

**[← Anterior: Control Hub](./control-hub.md)** | **[→ Siguiente: Driver Station](./driver-station.md)** | **[↑ Índice](../INTRO_INDICE.md)**
