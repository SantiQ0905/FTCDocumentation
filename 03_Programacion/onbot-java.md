# OnBot Java - Programación en Navegador

## Introducción

**OnBot Java** es un entorno de desarrollo Java basado en navegador web que permite escribir código Java directamente en el Control Hub sin necesidad de instalar Android Studio. Es ideal para equipos que quieren la potencia de Java sin la complejidad de configuración de Android Studio.

## Ventajas de OnBot Java

### Pros
- ✅ No requiere instalación de software
- ✅ Funciona en cualquier sistema operativo (Windows, Mac, Linux, Chrome OS)
- ✅ Compilación rápida directamente en el Control Hub
- ✅ Acceso completo al SDK de FTC
- ✅ Sintaxis completa de Java
- ✅ Compatible con la mayoría de librerías externas
- ✅ Múltiples usuarios pueden editar (con precaución)

### Contras
- ❌ Editor básico (sin IntelliSense avanzado)
- ❌ No tiene Git integration nativa
- ❌ Debugging limitado (solo telemetría)
- ❌ Autocompletado básico

## Acceso a OnBot Java

### Abrir el Editor

1. Conecta al Wi-Fi del Control Hub: `FTC-XXXX`
2. Abre navegador web (Chrome, Firefox, Edge recomendados)
3. Navega a: `http://192.168.43.1:8080`
4. Clic en **"OnBot Java"**

### Interfaz del Editor

```
┌──────────────────────────────────────────────────────────────┐
│ [+Nuevo] [📁Abrir] [💾Guardar] [🔨Build] [📱Deploy]        │
├──────────────┬───────────────────────────────────────────────┤
│  Archivos:   │  Editor de Código                             │
│  📁 java/    │                                                │
│  ├─ OpMode1  │  package org.firstinspires.ftc.teamcode;     │
│  ├─ OpMode2  │                                                │
│  └─ Utils    │  import com.qualcomm.robotcore...            │
│              │                                                │
│              │  @TeleOp(name="Mi OpMode")                    │
│              │  public class MiOpMode extends LinearOpMode { │
│              │      // Tu código aquí                        │
│              │  }                                             │
│              │                                                │
├──────────────┴───────────────────────────────────────────────┤
│ Console:                                                      │
│ BUILD SUCCESSFUL                                             │
└──────────────────────────────────────────────────────────────┘
```

## Crear tu Primer OpMode en OnBot Java

### Paso 1: Nuevo Archivo

1. Clic en **"+"** (Nuevo)
2. Tipo: **"OpMode"** → **"LinearOpMode"**
3. Nombre: `MiPrimerOpMode`
4. Categoría: **TeleOp** o **Autonomous**
5. Clic **"OK"**

OnBot Java genera automáticamente:

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;

@TeleOp(name="MiPrimerOpMode", group="Linear Opmode")
public class MiPrimerOpMode extends LinearOpMode {

    @Override
    public void runOpMode() {
        telemetry.addData("Status", "Initialized");
        telemetry.update();

        waitForStart();

        while (opModeIsActive()) {
            telemetry.addData("Status", "Running");
            telemetry.update();
        }
    }
}
```

### Paso 2: Agregar Hardware

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;

@TeleOp(name="Tank Drive", group="TeleOp")
public class TankDrive extends LinearOpMode {

    // Declarar hardware
    private DcMotor leftMotor = null;
    private DcMotor rightMotor = null;

    @Override
    public void runOpMode() {
        // Inicializar hardware
        leftMotor = hardwareMap.get(DcMotor.class, "leftMotor");
        rightMotor = hardwareMap.get(DcMotor.class, "rightMotor");

        // Configurar dirección
        leftMotor.setDirection(DcMotor.Direction.FORWARD);
        rightMotor.setDirection(DcMotor.Direction.REVERSE);

        telemetry.addData("Status", "Initialized");
        telemetry.update();

        waitForStart();

        // Loop principal
        while (opModeIsActive()) {
            double leftPower = -gamepad1.left_stick_y;
            double rightPower = -gamepad1.right_stick_y;

            leftMotor.setPower(leftPower);
            rightMotor.setPower(rightPower);

            telemetry.addData("Left Power", leftPower);
            telemetry.addData("Right Power", rightPower);
            telemetry.update();
        }
    }
}
```

### Paso 3: Compilar y Ejecutar

1. **Guardar**: Clic en 💾 o Ctrl+S
2. **Build**: Clic en 🔨 "Build Everything"
   - Espera a que compile (console inferior muestra progreso)
   - Errores aparecen en rojo con número de línea
3. **Ejecutar**: Abre Driver Station, selecciona tu OpMode, presiona INIT → START

## Estructura de Código Java en FTC

### Importaciones Comunes

```java
// OpMode basics
import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.eventloop.opmode.Autonomous;
import com.qualcomm.robotcore.eventloop.opmode.Disabled;

// Hardware
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.DcMotorSimple;
import com.qualcomm.robotcore.hardware.Servo;
import com.qualcomm.robotcore.hardware.ColorSensor;
import com.qualcomm.robotcore.hardware.DistanceSensor;

// Sensores avanzados
import com.qualcomm.hardware.bosch.BNO055IMU;
import org.firstinspires.ftc.robotcore.external.navigation.Orientation;
import org.firstinspires.ftc.robotcore.external.navigation.DistanceUnit;

// Utilidades
import com.qualcomm.robotcore.util.ElapsedTime;
import com.qualcomm.robotcore.util.Range;
```

### Anotaciones de OpMode

```java
// TeleOp
@TeleOp(name="Nombre del OpMode", group="Categoría")

// Autonomous
@Autonomous(name="Auto Rojo Izquierda", group="Autonomous")

// Desactivar OpMode (no aparece en lista)
@Disabled
@TeleOp(name="OpMode en Desarrollo", group="Test")
```

### Variables de Instancia

```java
public class MiOpMode extends LinearOpMode {

    // Hardware
    private DcMotor frontLeft, frontRight, backLeft, backRight;
    private Servo clawServo;
    private ColorSensor colorSensor;
    private BNO055IMU imu;

    // Variables de estado
    private double targetHeading = 0;
    private boolean clawOpen = false;

    // Constantes
    private static final double DRIVE_SPEED = 0.8;
    private static final double TURN_SPEED = 0.5;

    // Temporizadores
    private ElapsedTime runtime = new ElapsedTime();

    @Override
    public void runOpMode() {
        // Código del OpMode
    }
}
```

## Trabajar con Hardware

### Inicialización Completa de Motores

```java
private void initializeMotors() {
    frontLeft = hardwareMap.get(DcMotor.class, "frontLeft");
    frontRight = hardwareMap.get(DcMotor.class, "frontRight");
    backLeft = hardwareMap.get(DcMotor.class, "backLeft");
    backRight = hardwareMap.get(DcMotor.class, "backRight");

    // Dirección
    frontLeft.setDirection(DcMotor.Direction.REVERSE);
    backLeft.setDirection(DcMotor.Direction.REVERSE);
    frontRight.setDirection(DcMotor.Direction.FORWARD);
    backRight.setDirection(DcMotor.Direction.FORWARD);

    // Comportamiento al detenerse
    frontLeft.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    frontRight.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    backLeft.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);
    backRight.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);

    // Modo de encoder
    frontLeft.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    frontRight.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    backLeft.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    backRight.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
}
```

### Control Avanzado de Motores

#### Run to Position

```java
public void driveForward(double inches, double power) {
    int targetPosition = (int)(inches * COUNTS_PER_INCH);

    frontLeft.setTargetPosition(targetPosition);
    frontRight.setTargetPosition(targetPosition);
    backLeft.setTargetPosition(targetPosition);
    backRight.setTargetPosition(targetPosition);

    frontLeft.setMode(DcMotor.RunMode.RUN_TO_POSITION);
    frontRight.setMode(DcMotor.RunMode.RUN_TO_POSITION);
    backLeft.setMode(DcMotor.RunMode.RUN_TO_POSITION);
    backRight.setMode(DcMotor.RunMode.RUN_TO_POSITION);

    frontLeft.setPower(Math.abs(power));
    frontRight.setPower(Math.abs(power));
    backLeft.setPower(Math.abs(power));
    backRight.setPower(Math.abs(power));

    while (opModeIsActive() &&
           (frontLeft.isBusy() && frontRight.isBusy() &&
            backLeft.isBusy() && backRight.isBusy())) {

        telemetry.addData("Position", frontLeft.getCurrentPosition());
        telemetry.addData("Target", targetPosition);
        telemetry.update();
    }

    // Detener
    frontLeft.setPower(0);
    frontRight.setPower(0);
    backLeft.setPower(0);
    backRight.setPower(0);

    // Volver a modo normal
    frontLeft.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    frontRight.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    backLeft.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
    backRight.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
}
```

### Servos

```java
private Servo clawServo;
private Servo armServo;

private static final double CLAW_OPEN = 0.5;
private static final double CLAW_CLOSED = 0.0;

private void initializeServos() {
    clawServo = hardwareMap.get(Servo.class, "claw");
    armServo = hardwareMap.get(Servo.class, "arm");

    clawServo.setPosition(CLAW_OPEN);
}

// En loop de TeleOp
if (gamepad1.a) {
    clawServo.setPosition(CLAW_CLOSED);
} else if (gamepad1.b) {
    clawServo.setPosition(CLAW_OPEN);
}
```

### Sensores

#### Color Sensor

```java
private ColorSensor colorSensor;

colorSensor = hardwareMap.get(ColorSensor.class, "colorSensor");

// En loop
int red = colorSensor.red();
int green = colorSensor.green();
int blue = colorSensor.blue();

if (red > blue && red > green) {
    telemetry.addData("Color Detectado", "ROJO");
} else if (blue > red && blue > green) {
    telemetry.addData("Color Detectado", "AZUL");
}
```

#### Distance Sensor

```java
private DistanceSensor distanceSensor;

distanceSensor = hardwareMap.get(DistanceSensor.class, "distanceSensor");

// En loop
double distance = distanceSensor.getDistance(DistanceUnit.CM);

if (distance < 10) {
    telemetry.addData("Objeto", "CERCA");
} else {
    telemetry.addData("Distancia", "%.2f cm", distance);
}
```

## Organización de Código

### Crear Clase de Hardware

Archivo: `RobotHardware.java`

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.HardwareMap;
import com.qualcomm.robotcore.hardware.Servo;

public class RobotHardware {
    // Motores
    public DcMotor frontLeft = null;
    public DcMotor frontRight = null;
    public DcMotor backLeft = null;
    public DcMotor backRight = null;

    // Servos
    public Servo clawServo = null;

    // Constantes
    public static final double CLAW_OPEN = 0.5;
    public static final double CLAW_CLOSED = 0.0;

    private HardwareMap hwMap = null;

    public RobotHardware() {
        // Constructor vacío
    }

    public void init(HardwareMap ahwMap) {
        hwMap = ahwMap;

        // Inicializar motores
        frontLeft = hwMap.get(DcMotor.class, "frontLeft");
        frontRight = hwMap.get(DcMotor.class, "frontRight");
        backLeft = hwMap.get(DcMotor.class, "backLeft");
        backRight = hwMap.get(DcMotor.class, "backRight");

        frontLeft.setDirection(DcMotor.Direction.REVERSE);
        backLeft.setDirection(DcMotor.Direction.REVERSE);

        // Inicializar servos
        clawServo = hwMap.get(Servo.class, "claw");
        clawServo.setPosition(CLAW_OPEN);
    }
}
```

### Usar la Clase de Hardware

Archivo: `MiOpMode.java`

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;

@TeleOp(name="OpMode con Hardware Class", group="TeleOp")
public class MiOpMode extends LinearOpMode {

    private RobotHardware robot = new RobotHardware();

    @Override
    public void runOpMode() {
        robot.init(hardwareMap);

        waitForStart();

        while (opModeIsActive()) {
            double leftPower = -gamepad1.left_stick_y;
            double rightPower = -gamepad1.right_stick_y;

            robot.frontLeft.setPower(leftPower);
            robot.backLeft.setPower(leftPower);
            robot.frontRight.setPower(rightPower);
            robot.backRight.setPower(rightPower);

            if (gamepad1.a) {
                robot.clawServo.setPosition(RobotHardware.CLAW_CLOSED);
            } else if (gamepad1.b) {
                robot.clawServo.setPosition(RobotHardware.CLAW_OPEN);
            }

            telemetry.update();
        }
    }
}
```

## Consejos de OnBot Java

### Atajos de Teclado

- **Ctrl + S**: Guardar
- **Ctrl + F**: Buscar
- **Ctrl + H**: Buscar y reemplazar
- **Ctrl + /**: Comentar/descomentar línea

### Autocompletado

- Escribe parte del nombre y presiona **Ctrl + Espacio**
- OnBot Java muestra sugerencias básicas

### Debugging

OnBot Java no tiene debugger, usa telemetría:

```java
telemetry.addData("Debug - leftPower", leftPower);
telemetry.addData("Debug - Motor Position", motor.getCurrentPosition());
telemetry.addData("Debug - Sensor Value", sensor.getValue());
telemetry.update();
```

### Manejo de Errores

```java
try {
    motor = hardwareMap.get(DcMotor.class, "motor");
} catch (Exception e) {
    telemetry.addData("ERROR", "Motor no encontrado");
    telemetry.update();
}
```

## Backup y Control de Versiones

### Exportar Código

OnBot Java guarda archivos en el Control Hub. Para backup:

**Opción 1: Copiar Manualmente**
1. Selecciona todo el código (Ctrl + A)
2. Copia (Ctrl + C)
3. Pega en archivo local (.txt o .java)

**Opción 2: ADB**

```bash
adb pull /sdcard/FIRST/java/src/org/firstinspires/ftc/teamcode ./backup
```

### Usar Git (Avanzado)

Para usar Git con OnBot Java:

1. Exporta código a carpeta local
2. Inicializa repositorio Git
3. Commit cambios regularmente
4. Copia código de vuelta a OnBot Java cuando necesites

## Comparación: OnBot Java vs Android Studio

| Característica | OnBot Java | Android Studio |
|----------------|------------|----------------|
| Instalación | No requiere | Requiere |
| Plataforma | Cualquiera (navegador) | Windows/Mac/Linux |
| Compilación | En Control Hub | En laptop |
| Velocidad | Rápida | Más lenta |
| Editor | Básico | Avanzado (IntelliSense) |
| Debugging | Telemetría | Debugger completo |
| Git | Manual | Integrado |
| Librerías Externas | Limitado | Completo |

## Cuándo Usar OnBot Java

### Ideal Para:
- Equipos que no pueden instalar Android Studio
- Desarrollo rápido en competencias
- Cambios pequeños y pruebas
- Equipos con Chromebooks o tablets
- Cuando múltiples personas necesitan editar

### No Ideal Para:
- Proyectos grandes con muchos archivos
- Uso intensivo de librerías externas
- Desarrollo de algoritmos complejos que requieren debugging
- Equipos que quieren control de versiones robusto

## Próximos Pasos

- [Android Studio](./android-studio.md) - Entorno avanzado de desarrollo
- [Estructura OpMode](./estructura-opmode.md) - Entender OpModes en profundidad
- [Conceptos Básicos de Programación](./conceptos-basicos.md) - PID, state machines, etc.

---

**[← Anterior: Blocks](./blocks-programming.md)** | **[→ Siguiente: Android Studio](./android-studio.md)** | **[↑ Índice](../INTRO_INDICE.md)**
