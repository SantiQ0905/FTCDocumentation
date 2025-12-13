# Control Hub - El Cerebro del Robot FTC

## Introducción

El **REV Control Hub (REV-31-1595)** es el componente central de control para robots FTC modernos. Combina un procesador Android, hubs de expansión de I/O, IMU integrada, y conectividad Wi-Fi en un solo dispositivo compacto y robusto.

## Especificaciones Técnicas

### Hardware del Procesador

- **SoC**: Qualcomm Snapdragon 845
- **CPU**: Octa-core Kryo 385 (4x 2.8 GHz + 4x 1.8 GHz)
- **GPU**: Adreno 630
- **RAM**: 4 GB LPDDR4X
- **Almacenamiento**: 16 GB eMMC
- **Sistema Operativo**: Android 8.1 Oreo

### Puertos y Conectividad

#### Puertos de Motor

- **Cantidad**: 4 puertos de motor DC
- **Corriente Máxima**: 10A continuo por motor, 15A pico
- **Voltaje**: 12V nominal
- **Tipo de Conector**: JST VH 2-pin
- **Control**: PWM con retroalimentación de encoder

#### Puertos de Servo

- **Cantidad**: 6 puertos PWM
- **Voltaje de Salida**: 5V
- **Corriente Total**: 6A compartidos entre todos los servos
- **Tipo de Conector**: JST PH 3-pin (GND, VCC, Signal)
- **Rango PWM**: 600μs - 2400μs típico

#### Puertos de Sensor

**I2C:**
- **Cantidad**: 4 buses I2C independientes (Bus 0, 1, 2, 3)
- **Velocidad**: 100 kHz o 400 kHz
- **Voltaje**: 3.3V o 5V (configurable por bus)
- **Tipo de Conector**: JST PH 4-pin

**Digital I/O:**
- **Cantidad**: 8 puertos digitales
- **Voltaje**: 5V
- **Tipo**: Entrada/Salida configurable
- **Usos**: Encoders externos, sensores digitales, limitadores

**Analog Input:**
- **Cantidad**: 4 puertos analógicos
- **Resolución**: 12-bit (0-4095)
- **Rango de Voltaje**: 0-5V
- **Tipo de Conector**: JST PH 3-pin

### IMU Integrada

- **Modelo**: Bosch BNO055
- **Tipo**: 9-axis Absolute Orientation Sensor
- **Componentes**:
  - Acelerómetro de 3 ejes (±16g)
  - Giroscopio de 3 ejes (±2000°/s)
  - Magnetómetro de 3 ejes
- **Fusión de Sensores**: Procesamiento interno para orientación absoluta
- **Frecuencia de Actualización**: Hasta 100 Hz
- **Precisión de Heading**: ±1° (con calibración)

### Conectividad

**Wi-Fi:**
- **Estándar**: 802.11 a/b/g/n/ac
- **Frecuencias**: 2.4 GHz y 5 GHz
- **Modo**: Wi-Fi Direct (AP mode)
- **Rango**: ~30m en campo abierto (varía según interferencia)
- **Canales**: Configurables (automático por defecto)

**USB:**
- **Puerto Principal**: USB-C (OTG)
- **Usos**: Programación, debugging, conexión a webcam
- **Velocidad**: USB 3.0

**RS485:**
- **Puerto**: Mini JST para Expansion Hub
- **Uso**: Comunicación con Expansion Hub adicional
- **Velocidad**: 115200 baud

### Alimentación

- **Conector de Batería**: XT30 (macho)
- **Voltaje de Entrada**: 12V nominal (rango: 10.5V - 14V)
- **Consumo Típico**: 1-2A (sin carga en motores)
- **Consumo Máximo**: 50A total (limitado por fusible interno)
- **Protección**: Fusible auto-reseteable 20A para lógica

## Arquitectura del Sistema

### Diagrama de Bloques

```
┌─────────────────────────────────────────────────────────┐
│                    CONTROL HUB                          │
│                                                         │
│  ┌──────────────┐        ┌─────────────────┐          │
│  │  Snapdragon  │◄──────►│  Expansion Hub  │          │
│  │     845      │        │     Logic       │          │
│  │   (Android)  │        └────────┬────────┘          │
│  └──────┬───────┘                 │                    │
│         │                         │                    │
│   ┌─────▼─────┐          ┌────────▼────────┐          │
│   │  Wi-Fi    │          │  Motor Drivers  │          │
│   │  Module   │          │  Servo Outputs  │          │
│   └───────────┘          │  Sensor Ports   │          │
│                          └─────────────────┘          │
│                                                         │
│   [XT30]  [USB-C]  [RS485]                            │
└─────────────────────────────────────────────────────────┘
```

### Flujo de Datos

1. **Driver Station** envía comandos vía Wi-Fi al **Control Hub**
2. **Android OS** ejecuta el OpMode (código Java)
3. **Hardware Abstraction Layer** traduce comandos a señales hardware
4. **Motor Controllers** y **Servo PWM** ejecutan las acciones
5. **Sensores** envían datos de vuelta al OpMode
6. **Telemetría** se envía al Driver Station para visualización

## Configuración y Uso

### Configuración Inicial

#### Primer Encendido

1. **Conectar Batería**:
   - Asegura que la batería esté cargada (>12V)
   - Conecta el conector XT30
   - El LED de estado parpadeará

2. **Secuencia de Arranque**:
   - LED Rojo: Encendiendo (5-10 segundos)
   - LED Naranja: Cargando sistema Android (20-40 segundos)
   - LED Verde Parpadeante: Listo para conexión
   - LED Verde Fijo: Driver Station conectado

3. **Apagar Correctamente**:
   - Mantén presionado el botón de encendido por 3 segundos
   - El LED se volverá rojo
   - Espera a que el LED se apague completamente
   - Desconecta la batería

### Acceso a la Interfaz Web

#### Conectar vía Wi-Fi

1. En tu laptop/tablet, busca la red Wi-Fi: `FTC-XXXX`
   - XXXX = últimos 4 dígitos del número de serie
2. Contraseña por defecto: Ver etiqueta del Control Hub o `password`
3. Abre navegador web: `http://192.168.43.1:8080`

#### Interfaz de Programación

La interfaz web del Control Hub ofrece:

- **Program & Manage**:
  - OnBot Java: Editor de código Java en navegador
  - Blocks: Programación visual
  - Manage: Actualización de firmware y configuración

- **Self Inspect**:
  - Diagnóstico del hardware
  - Estado de puertos
  - Voltaje de batería

- **Configure Robot**:
  - Mapeo de hardware
  - Configuración de sensores
  - Calibración de IMU

### Configuración de Hardware

#### Crear Configuración de Hardware

1. En la interfaz web o Driver Station, navega a "Configure Robot"
2. Toca "New" para crear nueva configuración
3. Nombre descriptivo: `MyRobotConfig` o número de equipo
4. Selecciona "Control Hub Portal"
5. El sistema escaneará automáticamente dispositivos conectados

#### Mapeo de Dispositivos

**Motores:**
```
Port 0: frontLeftMotor    (goBILDA 5203-2402-0001)
Port 1: frontRightMotor   (goBILDA 5203-2402-0001)
Port 2: backLeftMotor     (REV HD Hex Motor)
Port 3: backRightMotor    (REV HD Hex Motor)
```

**Servos:**
```
Port 0: clawServo        (Servo)
Port 1: armServo         (Servo)
Port 2: intakeServo      (Continuous Rotation Servo)
```

**Sensores I2C:**
```
I2C Bus 0:
  - imu (Embedded IMU)

I2C Bus 1:
  - colorSensor (REV Color Sensor V3)

I2C Bus 2:
  - distanceSensor (REV 2m Distance Sensor)
```

**Sensores Digitales:**
```
Port 0-1: leftEncoder  (Encoder)
Port 2-3: rightEncoder (Encoder)
Port 4:   touchSensor  (Digital Device)
```

#### Guardar y Activar

1. Toca "Done" para guardar
2. La configuración se almacena en: `/sdcard/FIRST/settings/`
3. Activa la configuración en el Driver Station
4. Verifica que todos los dispositivos aparezcan en telemetría

### Calibración de la IMU

#### ¿Por Qué Calibrar?

La IMU del Control Hub necesita calibración para:
- Compensar campos magnéticos locales
- Ajustar offsets de sensores
- Maximizar precisión de orientación

#### Procedimiento de Calibración

**Método 1: Mediante OpMode**

```java
@Autonomous(name="Calibrar IMU", group="Calibration")
public class CalibrateIMU extends LinearOpMode {

    BNO055IMU imu;

    @Override
    public void runOpMode() {
        // Inicializar IMU
        BNO055IMU.Parameters parameters = new BNO055IMU.Parameters();
        parameters.angleUnit = BNO055IMU.AngleUnit.DEGREES;
        parameters.accelUnit = BNO055IMU.AccelUnit.METERS_PERSEC_PERSEC;
        parameters.calibrationDataFile = "BNO055IMUCalibration.json";
        parameters.loggingEnabled = true;
        parameters.loggingTag = "IMU";

        imu = hardwareMap.get(BNO055IMU.class, "imu");
        imu.initialize(parameters);

        telemetry.addData("Status", "Calibrando IMU...");
        telemetry.update();

        // Esperar a calibración
        while (!isStopRequested() && !imu.isGyroCalibrated()) {
            sleep(50);
            telemetry.addData("Calibration Status", imu.getCalibrationStatus());
            telemetry.update();
        }

        telemetry.addData("IMU", "Calibrado!");
        telemetry.update();

        waitForStart();

        // Guardar datos de calibración
        BNO055IMU.CalibrationData calibrationData = imu.readCalibrationData();

        // Mostrar orientación
        while (opModeIsActive()) {
            Orientation angles = imu.getAngularOrientation(
                AxesReference.INTRINSIC,
                AxesOrder.ZYX,
                AngleUnit.DEGREES
            );

            telemetry.addData("Heading", angles.firstAngle);
            telemetry.addData("Roll", angles.secondAngle);
            telemetry.addData("Pitch", angles.thirdAngle);
            telemetry.update();
        }
    }
}
```

**Método 2: Calibración Manual**

1. Coloca el robot en superficie plana y nivelada
2. Asegura que no haya objetos metálicos cerca
3. Ejecuta el OpMode de calibración
4. Sigue las instrucciones en pantalla:
   - Mantén el robot quieto (giroscopio)
   - Gira lentamente 360° (magnetómetro)
   - Inclina suavemente (acelerómetro)
5. Los datos se guardan automáticamente

#### Verificar Calibración

```java
BNO055IMU.CalibrationStatus status = imu.getCalibrationStatus();
telemetry.addData("Gyro", status.gyroCalibrated ? "OK" : "Calibrando...");
telemetry.addData("Accel", status.accelCalibrated ? "OK" : "Calibrando...");
telemetry.addData("Mag", status.magCalibrated ? "OK" : "Calibrando...");
telemetry.update();
```

### Actualización de Firmware

#### ¿Cuándo Actualizar?

- Inicio de cada temporada
- Cuando hay bugs conocidos solucionados
- Para nuevas características
- Cuando lo requiere el Game Manual

#### Proceso de Actualización

**1. Descargar Firmware Más Reciente**

- Visita: [GitHub FIRST Tech Challenge](https://github.com/FIRST-Tech-Challenge/FtcRobotController/releases)
- Descarga el archivo APK más reciente (ejemplo: `FtcRobotController-v8.2.apk`)

**2. Actualizar Robot Controller App**

1. Conecta al Wi-Fi del Control Hub
2. Navega a `192.168.43.1:8080`
3. Clic en "Manage" → "Update Robot Controller App"
4. Selecciona el archivo APK descargado
5. Espera a que se instale (2-5 minutos)
6. El Control Hub se reiniciará automáticamente

**3. Actualizar Expansion Hub Firmware** (si aplica)

1. En "Manage" → "Update Expansion Hub Firmware"
2. Selecciona el archivo `.bin` incluido en el release
3. Sigue las instrucciones en pantalla
4. **No desconectes la batería** durante el proceso

**4. Verificar Versión**

- En la interfaz web, la versión aparece en la parte superior
- En Driver Station: Menú → About

## Programación del Control Hub

### Acceder al Hardware en Código

#### Inicializar Motores

```java
DcMotor frontLeft = hardwareMap.get(DcMotor.class, "frontLeftMotor");
frontLeft.setDirection(DcMotor.Direction.FORWARD);
frontLeft.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
frontLeft.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
```

#### Controlar Servos

```java
Servo clawServo = hardwareMap.get(Servo.class, "clawServo");
clawServo.setPosition(0.5);  // Rango: 0.0 - 1.0
```

#### Leer Sensores

```java
// Color Sensor
ColorSensor colorSensor = hardwareMap.get(ColorSensor.class, "colorSensor");
int red = colorSensor.red();
int blue = colorSensor.blue();

// Distance Sensor
DistanceSensor distanceSensor = hardwareMap.get(DistanceSensor.class, "distanceSensor");
double distance = distanceSensor.getDistance(DistanceUnit.CM);

// IMU
BNO055IMU imu = hardwareMap.get(BNO055IMU.class, "imu");
Orientation angles = imu.getAngularOrientation(...);
```

### Uso Avanzado de la IMU

#### Obtener Orientación Absoluta

```java
// En runOpMode()
Orientation angles = imu.getAngularOrientation(
    AxesReference.INTRINSIC,
    AxesOrder.ZYX,
    AngleUnit.DEGREES
);

double heading = angles.firstAngle;   // Yaw (rotación Z)
double roll = angles.secondAngle;     // Roll (rotación Y)
double pitch = angles.thirdAngle;     // Pitch (rotación X)
```

#### Calcular Cambio de Ángulo

```java
private double lastHeading = 0;

public double getHeadingChange() {
    Orientation angles = imu.getAngularOrientation(
        AxesReference.INTRINSIC,
        AxesOrder.ZYX,
        AngleUnit.DEGREES
    );

    double currentHeading = angles.firstAngle;
    double change = currentHeading - lastHeading;

    // Normalizar a -180 a 180
    while (change > 180) change -= 360;
    while (change < -180) change += 360;

    lastHeading = currentHeading;
    return change;
}
```

#### Navegación con IMU

```java
// Girar a ángulo específico
public void turnToHeading(double targetHeading, double power) {
    Orientation angles = imu.getAngularOrientation(...);
    double currentHeading = angles.firstAngle;

    double error = targetHeading - currentHeading;

    // Normalizar error
    while (error > 180) error -= 360;
    while (error < -180) error += 360;

    // Girar basado en error
    if (Math.abs(error) > 2) {  // Tolerancia de 2 grados
        double turnPower = error > 0 ? power : -power;
        // Aplicar potencia a motores para girar
    }
}
```

## Diagnóstico y Troubleshooting

### LEDs de Estado

| Color LED | Estado | Significado |
|-----------|--------|-------------|
| Rojo | Encendido | Iniciando sistema |
| Naranja | Encendido | Cargando Android |
| Verde Parpadeante | Lento | Listo, esperando conexión |
| Verde Parpadeante | Rápido | Driver Station conectado, esperando INIT |
| Verde | Fijo | OpMode en ejecución |
| Rojo Parpadeante | - | Error crítico |

### Problemas Comunes

#### No Enciende

**Síntomas**: LED no se enciende al presionar botón

**Soluciones**:
1. Verifica batería cargada (>12V con multímetro)
2. Verifica conexión XT30 firme
3. Verifica fusible interno (requiere desarmar, contacta REV)
4. Prueba con otra batería

#### No Conecta Wi-Fi

**Síntomas**: Red Wi-Fi no aparece o no conecta

**Soluciones**:
1. Espera 60 segundos después de encender
2. Olvida la red en tu dispositivo y reconecta
3. Verifica que no haya múltiples Control Hubs cerca (interferencia)
4. Cambia el canal Wi-Fi en configuración avanzada
5. Factory reset del Control Hub

#### Motores No Responden

**Síntomas**: Código ejecuta pero motores no se mueven

**Diagnóstico**:
1. Verifica voltaje de batería en Driver Station (>12V)
2. Revisa conexiones físicas de motores
3. Usa "Self Inspect" para verificar puertos
4. Prueba motores en diferentes puertos
5. Verifica que `setPower()` se llame con valores != 0

**Código de Prueba**:
```java
// En teleOp loop
if (gamepad1.a) {
    frontLeft.setPower(0.5);
    telemetry.addData("Motor Test", "Running at 50%");
} else {
    frontLeft.setPower(0);
    telemetry.addData("Motor Test", "Stopped");
}
telemetry.update();
```

#### IMU No Calibra

**Síntomas**: `imu.isGyroCalibrated()` siempre devuelve false

**Soluciones**:
1. Coloca robot en superficie completamente plana
2. Aleja objetos metálicos y magnéticos
3. Mantén robot completamente quieto durante calibración
4. Reinicia Control Hub
5. Elimina archivo de calibración: `/sdcard/FIRST/settings/BNO055IMUCalibration.json`

#### Pérdida de Conexión Durante Partido

**Síntomas**: Conexión Wi-Fi se pierde intermitentemente

**Soluciones**:
1. Verifica que la antena esté conectada firmemente
2. Reduce interferencia: alejar de otros dispositivos Wi-Fi
3. Cambia canal Wi-Fi a uno menos congestionado
4. Acorta distancia entre Control Hub y Driver Station
5. Asegura que la batería mantenga >12V bajo carga

### Herramientas de Diagnóstico

#### Self Inspect

Acceder: Interfaz web → "Self Inspect"

Muestra:
- Estado de cada puerto de motor
- Voltaje de batería en tiempo real
- Estado de sensores I2C
- Temperatura del procesador
- Estado de memoria y almacenamiento

#### Telemetría Avanzada

```java
// Agregar información de diagnóstico
telemetry.addData("Battery Voltage", "%.2f V",
    hardwareMap.voltageSensor.iterator().next().getVoltage());
telemetry.addData("Frequency (loops/sec)", "%.1f",
    1000.0 / loopTime);

// Estado de motores
telemetry.addData("Front Left", "Power: %.2f, Pos: %d",
    frontLeft.getPower(), frontLeft.getCurrentPosition());
```

## Mantenimiento

### Rutina Regular

**Antes de Cada Competencia:**
- [ ] Verificar firmware actualizado
- [ ] Limpiar puertos de polvo/suciedad
- [ ] Verificar conexiones firmes
- [ ] Calibrar IMU
- [ ] Probar todos los puertos con OpMode de diagnóstico
- [ ] Verificar temperatura bajo carga (no debe exceder 60°C)

**Mensual:**
- [ ] Limpiar con aire comprimido (baja presión)
- [ ] Verificar montaje seguro en robot
- [ ] Revisar integridad de conectores
- [ ] Backup de configuraciones

### Almacenamiento

- Almacenar en lugar seco, temperatura ambiente
- No exponer a temperaturas extremas (<0°C o >40°C)
- Desconectar batería si no se usa por >1 semana
- Proteger de golpes e impactos

## Próximos Pasos

- [Expansion Hub](./expansion-hub.md) - Ampliar capacidades del robot
- [Driver Station](./driver-station.md) - Configurar la estación de control
- [Comunicaciones](./comunicaciones.md) - Optimizar conexión Wi-Fi
- [Sistema Eléctrico](../04_Sistema_Electrico/alimentacion.md) - Gestión de energía

---

**[← Volver al Índice](../INTRO_INDICE.md)** | **[→ Siguiente: Expansion Hub](./expansion-hub.md)**
