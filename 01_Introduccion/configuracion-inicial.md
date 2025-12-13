# Configuración Inicial del Robot FTC

## Introducción

Esta guía te llevará paso a paso a través del proceso de configuración inicial de tu robot FTC, desde desempacar los componentes hasta ejecutar tu primer OpMode.

## Pre-Requisitos

Antes de comenzar, asegúrate de tener:

- [ ] Control Hub o Robot Controller Phone
- [ ] Expansion Hub (opcional)
- [ ] Driver Station (teléfono/tablet Android)
- [ ] Batería de 12V completamente cargada
- [ ] Cable USB-A a USB-C (para Control Hub)
- [ ] Laptop con conexión a internet
- [ ] Al menos 2 motores DC
- [ ] Al menos 2 servos
- [ ] Gamepad compatible

## Paso 1: Actualizar el Software

### 1.1 Descargar la App del Control Hub

**En tu Driver Station:**

1. Abre Google Play Store
2. Busca "FTC Driver Station"
3. Instala la aplicación oficial de FIRST
4. Alternativamente, descarga el APK desde [GitHub de FIRST Tech Challenge](https://github.com/FIRST-Tech-Challenge/FtcRobotController)

### 1.2 Actualizar el Control Hub

**Importante**: Siempre usa la versión más reciente del SDK de FTC.

1. Conecta el Control Hub a tu laptop vía USB
2. Abre un navegador web y navega a: `192.168.43.1:8080` (dirección por defecto)
3. Si no funciona, conecta vía Wi-Fi Direct:
   - En tu laptop, busca la red Wi-Fi del Control Hub (FTC-XXXX)
   - Contraseña por defecto en la etiqueta del Control Hub
4. En la interfaz web:
   - Selecciona "Manage" en el menú
   - Clic en "Update Robot Controller App"
   - Sube el archivo APK más reciente

### 1.3 Verificar Versión del Firmware

1. En la interfaz web del Control Hub: `192.168.43.1:8080`
2. Verifica que la versión del firmware sea compatible con el SDK
3. Si necesita actualización:
   - Navega a "Manage"
   - Selecciona "Update Expansion Hub Firmware"
   - Sigue las instrucciones en pantalla

## Paso 2: Conectar el Hardware

### 2.1 Diagrama de Conexión Básico

```
[Batería 12V] ---[XT30]---> [Control Hub]
                                  |
                    +-------------+-------------+
                    |             |             |
                 [Motor 0]    [Motor 1]    [Servo 0]
```

### 2.2 Conectar la Batería

1. **Apaga** el Control Hub si está encendido
2. Conecta el conector XT30 de la batería al Control Hub
3. Asegura la batería al chasis con velcro o amarres
4. **No enciendas** aún el Control Hub

### 2.3 Conectar Motores

**Para cada motor:**

1. Identifica los cables del motor (2 cables, generalmente rojo y negro)
2. Conecta al puerto de motor del Control Hub:
   - Puerto 0: Motor izquierdo (ejemplo)
   - Puerto 1: Motor derecho (ejemplo)
   - Puerto 2: Motor adicional
   - Puerto 3: Motor adicional
3. Asegura los cables con amarres para evitar desconexiones

**Notas:**
- La polaridad determina la dirección de rotación
- Puedes invertir en software si es necesario

### 2.4 Conectar Servos

**Para cada servo:**

1. Conecta el cable de 3 pines (marrón/rojo/naranja o negro/rojo/blanco)
2. Puertos de servo en el Control Hub (0-5)
3. Orientación correcta:
   - Marrón/Negro = GND (hacia el lado marcado)
   - Rojo = VCC (centro)
   - Naranja/Blanco = Señal

### 2.5 Conectar Sensores

#### Sensor I2C (ejemplo: Color Sensor V3)

1. Conecta al puerto I2C del Control Hub (0-3)
2. Cable de 4 pines: GND, VCC, SDA, SCL
3. Asegura la conexión

#### Sensor Digital (ejemplo: Touch Sensor)

1. Conecta al puerto Digital del Control Hub
2. Verifica la orientación correcta

## Paso 3: Configuración del Hardware

### 3.1 Encender el Control Hub

1. Presiona el botón de encendido en el Control Hub
2. Espera a que la luz LED se vuelva verde (puede tomar 30-60 segundos)
3. El LED parpadeante indica que está listo

### 3.2 Conectar el Driver Station

#### Opción A: Wi-Fi Direct

1. En el Driver Station, abre "Configuración de Wi-Fi"
2. Busca la red `FTC-XXXX` (XXXX = últimos 4 dígitos del número de serie)
3. Conéctate usando la contraseña (en la etiqueta del Control Hub o por defecto: `password`)
4. Abre la app "FTC Driver Station"
5. Debe conectarse automáticamente al Control Hub

#### Opción B: USB (Solo para Programación)

1. Conecta el Driver Station al Control Hub vía USB-C
2. Autoriza la conexión USB en el Driver Station
3. Abre la app "FTC Driver Station"

### 3.3 Configurar Hardware en el Robot

1. En el Driver Station, toca el menú (tres puntos) en la esquina superior derecha
2. Selecciona "Configure Robot"
3. Crea una nueva configuración:
   - Toca el botón "New"
   - Nombre: "RobotConfig" (o el nombre de tu equipo)
4. Selecciona "Control Hub Portal"
5. Escanea los dispositivos:
   - El Control Hub detectará automáticamente los dispositivos conectados

### 3.4 Mapear Dispositivos

#### Configurar Motores

Para cada motor conectado:

1. En la configuración, expande "Motors"
2. Selecciona el puerto (0, 1, 2, 3)
3. Asigna un nombre descriptivo:
   - Ejemplo: `leftFront`, `rightFront`, `leftRear`, `rightRear`
4. Selecciona el tipo de motor:
   - "goBILDA 5202/3/4 series"
   - "REV HD Hex"
   - "REV Core Hex"
   - Etc.
5. Configura dirección si es necesario (se puede hacer en código también)

#### Configurar Servos

Para cada servo:

1. Expande "Servos"
2. Selecciona el puerto (0-5)
3. Asigna nombre: ejemplo `clawServo`, `armServo`
4. Tipo: "Servo" (estándar) o "Continuous Rotation Servo"

#### Configurar Sensores

**Para sensores I2C (ejemplo: Color Sensor):**

1. Expande el puerto I2C correspondiente (Bus 0, 1, 2, 3)
2. Selecciona el dispositivo detectado
3. Asigna nombre: `colorSensor`, `distanceSensor`
4. Tipo: "REV Color/Range Sensor"

**Para sensores digitales:**

1. Expande "Digital Devices"
2. Selecciona el puerto
3. Asigna nombre: `touchSensor`
4. Tipo: "Digital Device" o específico del sensor

#### Configurar IMU

1. Expande "I2C Bus 0"
2. Busca "Embedded IMU"
3. Asigna nombre: `imu`
4. Esta es la IMU integrada en el Control Hub

### 3.5 Guardar Configuración

1. Toca "Done" en la esquina superior derecha
2. Confirma que quieres guardar
3. La configuración se almacena en el Control Hub

## Paso 4: Instalar SDK y Entorno de Desarrollo

### 4.1 Opción 1: OnBot Java (Más Simple)

**Ventajas**: No requiere instalación, funciona en navegador

1. Conecta tu laptop al Wi-Fi del Control Hub
2. Abre navegador: `192.168.43.1:8080`
3. Clic en "OnBot Java"
4. Listo para programar

### 4.2 Opción 2: Blocks (Para Principiantes)

**Ventajas**: Programación visual, ideal para aprender

1. Conecta laptop al Wi-Fi del Control Hub
2. Abre navegador: `192.168.43.1:8080`
3. Clic en "Blocks"
4. Arrastra y suelta bloques para programar

### 4.3 Opción 3: Android Studio (Avanzado)

**Ventajas**: Control completo, debugging avanzado, Git integration

#### Requisitos del Sistema

- **OS**: Windows 10/11, macOS, o Linux
- **RAM**: Mínimo 8GB (recomendado 16GB)
- **Almacenamiento**: 10GB libres
- **Java**: JDK 11 o superior

#### Pasos de Instalación

1. **Descargar Android Studio**
   - Visita: [developer.android.com/studio](https://developer.android.com/studio)
   - Descarga la versión más reciente
   - Instala siguiendo el wizard

2. **Descargar FtcRobotController**
   ```bash
   git clone https://github.com/FIRST-Tech-Challenge/FtcRobotController.git
   ```
   - O descarga el ZIP desde GitHub

3. **Abrir Proyecto en Android Studio**
   - Abre Android Studio
   - File → Open
   - Selecciona la carpeta `FtcRobotController`
   - Espera a que Gradle sincronice (puede tomar varios minutos)

4. **Configurar SDK de Android**
   - Tools → SDK Manager
   - Instala Android 8.0 (API 26) o superior
   - Instala Build Tools más recientes

5. **Configurar ADB**
   - Habilita "Developer Options" en tu Driver Station
   - Habilita "USB Debugging"
   - Conecta vía USB y autoriza la computadora

## Paso 5: Programar tu Primer OpMode

### 5.1 ¿Qué es un OpMode?

Un **OpMode** (Operation Mode) es un programa que ejecuta tu robot. Hay dos tipos principales:

- **TeleOp**: Controlado por humanos con gamepad
- **Autonomous**: El robot opera solo, sin intervención

### 5.2 Crear un OpMode Simple (OnBot Java)

1. En OnBot Java, clic en el signo "+"
2. Selecciona "OpMode"
3. Nombre: `MyFirstOpMode`
4. Tipo: `TeleOp`

**Código de ejemplo:**

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;

@TeleOp(name="Mi Primer OpMode", group="Linear Opmode")
public class MyFirstOpMode extends LinearOpMode {

    // Declarar motores
    private DcMotor leftMotor = null;
    private DcMotor rightMotor = null;

    @Override
    public void runOpMode() {

        // Inicializar hardware
        leftMotor = hardwareMap.get(DcMotor.class, "leftMotor");
        rightMotor = hardwareMap.get(DcMotor.class, "rightMotor");

        // Configurar dirección de motores
        leftMotor.setDirection(DcMotor.Direction.FORWARD);
        rightMotor.setDirection(DcMotor.Direction.REVERSE);

        // Esperar a que el conductor presione PLAY
        telemetry.addData("Status", "Inicializado");
        telemetry.update();

        waitForStart();

        // Bucle principal
        while (opModeIsActive()) {

            // Control de tanque simple
            double leftPower = -gamepad1.left_stick_y;
            double rightPower = -gamepad1.right_stick_y;

            // Enviar potencia a los motores
            leftMotor.setPower(leftPower);
            rightMotor.setPower(rightPower);

            // Mostrar información
            telemetry.addData("Left Power", leftPower);
            telemetry.addData("Right Power", rightPower);
            telemetry.update();
        }
    }
}
```

### 5.3 Construir y Desplegar

**OnBot Java:**
1. Clic en "Build Everything"
2. Espera a que compile (ver console abajo)
3. Si hay errores, revisa el código

**Android Studio:**
1. Conecta Driver Station o Control Hub vía USB
2. Selecciona el dispositivo en la barra superior
3. Clic en el botón "Run" (triángulo verde)
4. Espera a que compile e instale

## Paso 6: Ejecutar el OpMode

### 6.1 En el Driver Station

1. Conecta tu gamepad al Driver Station
2. Abre la app "FTC Driver Station"
3. Verifica la conexión (debe mostrar el voltaje de la batería)
4. En el menú desplegable de OpMode, selecciona "Mi Primer OpMode"
5. Presiona "INIT"
6. Espera a que el OpMode se inicialice (debe decir "Inicializado")
7. Presiona "START" (▶)

### 6.2 Controlar el Robot

1. Usa el joystick izquierdo del gamepad para el motor izquierdo
2. Usa el joystick derecho para el motor derecho
3. El robot debe moverse según tus comandos

### 6.3 Detener el OpMode

1. Presiona "STOP" (⏹) en el Driver Station
2. O presiona el botón de STOP en el gamepad

## Paso 7: Verificación y Troubleshooting

### Problemas Comunes

#### El Driver Station no se conecta al Control Hub

**Solución:**
- Verifica que ambos estén encendidos
- Reconecta al Wi-Fi del Control Hub
- Reinicia ambos dispositivos
- Verifica que estés usando la contraseña correcta

#### Los motores no se mueven

**Solución:**
- Verifica que la batería esté cargada (>12V)
- Comprueba las conexiones físicas
- Verifica que los nombres en el código coincidan con la configuración
- Revisa la dirección de los motores
- Asegúrate de que `setPower()` reciba valores != 0

#### Error: "Hardware map doesn't contain device"

**Solución:**
- Los nombres en el código deben coincidir EXACTAMENTE con la configuración
- Verifica mayúsculas/minúsculas
- Re-escanea el hardware en la configuración

#### El robot se mueve en dirección incorrecta

**Solución:**
- Invierte la dirección en código: `setDirection(DcMotor.Direction.REVERSE)`
- O cambia la polaridad del motor físicamente

#### OpMode no aparece en la lista

**Solución:**
- Verifica que el código compiló sin errores
- Asegúrate de tener la anotación `@TeleOp` o `@Autonomous`
- Reinicia la app del Driver Station
- Reconstruye el proyecto

### Verificación de Hardware

#### Probar Motores Individualmente

En OnBot Java o Android Studio, crea un OpMode de prueba:

```java
@TeleOp(name="Prueba de Motores", group="Test")
public class MotorTest extends LinearOpMode {
    @Override
    public void runOpMode() {
        DcMotor motor = hardwareMap.get(DcMotor.class, "motor0");

        waitForStart();

        while (opModeIsActive()) {
            if (gamepad1.a) {
                motor.setPower(0.5);  // 50% adelante
            } else if (gamepad1.b) {
                motor.setPower(-0.5); // 50% atrás
            } else {
                motor.setPower(0);    // Detener
            }

            telemetry.addData("Motor Power", motor.getPower());
            telemetry.update();
        }
    }
}
```

#### Probar Servos

```java
@TeleOp(name="Prueba de Servos", group="Test")
public class ServoTest extends LinearOpMode {
    @Override
    public void runOpMode() {
        Servo servo = hardwareMap.get(Servo.class, "servo0");

        waitForStart();

        while (opModeIsActive()) {
            if (gamepad1.dpad_up) {
                servo.setPosition(1.0);  // Máximo
            } else if (gamepad1.dpad_down) {
                servo.setPosition(0.0);  // Mínimo
            } else if (gamepad1.dpad_left) {
                servo.setPosition(0.5);  // Centro
            }

            telemetry.addData("Servo Position", servo.getPosition());
            telemetry.update();
        }
    }
}
```

## Paso 8: Mejores Prácticas

### Organización del Código

- Usa nombres descriptivos para variables y métodos
- Comenta tu código para futura referencia
- Separa la lógica en métodos reutilizables
- Usa constantes para valores que no cambian

### Gestión de Hardware

- Etiqueta todos los cables físicamente
- Documenta tu configuración en el Engineering Notebook
- Mantén un diagrama de cableado actualizado
- Usa amarres de cable para organización

### Seguridad

- **Nunca** toques el robot mientras está encendido y en modo RUN
- Siempre ten un botón de parada de emergencia accesible
- Asegura bien la batería
- Inspecciona cables regularmente por desgaste

### Control de Versiones

- Usa Git para gestionar tu código
- Crea branches para nuevas características
- Commit frecuentemente con mensajes descriptivos
- Haz backups regulares

## Próximos Pasos

Ahora que tienes tu robot configurado y funcionando:

- [Programación Básica](../03_Programacion/conceptos-basicos.md) - Aprende conceptos de programación FTC
- [Sistema de Control](../02_Sistema_Control/control-hub.md) - Profundiza en el Control Hub
- [Uso de Sensores](../04_Sistema_Electrico/sensores.md) - Integra sensores en tu código
- [FTCLib](../05_FTCLib/introduccion-ftclib.md) - Usa librerías avanzadas

---

**[← Volver al Índice](../INTRO_INDICE.md)** | **[→ Siguiente: Sistema de Control](../02_Sistema_Control/control-hub.md)**
