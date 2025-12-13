# Conceptos Básicos de Programación FTC

## Introducción

Este documento cubre conceptos fundamentales de programación que todo equipo de FTC debe conocer, desde control de motores hasta algoritmos avanzados.

## Control PID

### ¿Qué es PID?

**PID** (Proporcional-Integral-Derivativo) es un algoritmo de control que permite alcanzar y mantener una posición/velocidad objetivo.

### Componentes del PID

**P (Proporcional)**: Corrige proporcionalmente al error
```java
double error = target - current;
double output = Kp * error;
```

**I (Integral)**: Elimina error acumulado
```java
integralSum += error * deltaTime;
double output = Ki * integralSum;
```

**D (Derivativo)**: Reduce oscilaciones
```java
double derivative = (error - lastError) / deltaTime;
double output = Kd * derivative;
```

### Implementación Básica

```java
public class PIDController {
    private double Kp, Ki, Kd;
    private double integralSum = 0;
    private double lastError = 0;
    private ElapsedTime timer = new ElapsedTime();

    public PIDController(double kp, double ki, double kd) {
        this.Kp = kp;
        this.Ki = ki;
        this.Kd = kd;
    }

    public double calculate(double target, double current) {
        double error = target - current;
        double deltaTime = timer.seconds();

        // Proporcional
        double p = Kp * error;

        // Integral
        integralSum += error * deltaTime;
        double i = Ki * integralSum;

        // Derivativo
        double derivative = (error - lastError) / deltaTime;
        double d = Kd * derivative;

        lastError = error;
        timer.reset();

        return p + i + d;
    }
}
```

### Uso con Motor

```java
PIDController pid = new PIDController(0.01, 0.0, 0.001);

while (opModeIsActive()) {
    double targetPosition = 1000; // ticks de encoder
    double currentPosition = motor.getCurrentPosition();

    double power = pid.calculate(targetPosition, currentPosition);
    motor.setPower(Range.clip(power, -1.0, 1.0));

    telemetry.addData("Target", targetPosition);
    telemetry.addData("Current", currentPosition);
    telemetry.addData("Power", power);
    telemetry.update();
}
```

### Tuning PID

1. **Empezar con Kp**: Aumenta hasta que oscile
2. **Agregar Kd**: Reduce oscilaciones
3. **Agregar Ki**: Elimina error residual (usa con precaución)

**Valores típicos**:
- Kp: 0.001 - 0.1
- Ki: 0.0 - 0.01
- Kd: 0.0001 - 0.01

## State Machines (Máquinas de Estado)

### Concepto

Una state machine organiza lógica compleja en estados discretos.

### Implementación con Enum

```java
public class AutonomoStateMachine extends LinearOpMode {

    enum State {
        DRIVE_FORWARD,
        TURN_RIGHT,
        PLACE_OBJECT,
        PARK,
        STOP
    }

    private State currentState = State.DRIVE_FORWARD;
    private ElapsedTime stateTimer = new ElapsedTime();

    @Override
    public void runOpMode() {
        // Inicialización
        DcMotor leftMotor = hardwareMap.get(DcMotor.class, "left");
        DcMotor rightMotor = hardwareMap.get(DcMotor.class, "right");

        waitForStart();

        while (opModeIsActive() && currentState != State.STOP) {
            switch (currentState) {
                case DRIVE_FORWARD:
                    leftMotor.setPower(0.5);
                    rightMotor.setPower(0.5);

                    if (stateTimer.seconds() > 2.0) {
                        currentState = State.TURN_RIGHT;
                        stateTimer.reset();
                    }
                    break;

                case TURN_RIGHT:
                    leftMotor.setPower(0.5);
                    rightMotor.setPower(-0.5);

                    if (stateTimer.seconds() > 1.0) {
                        currentState = State.PLACE_OBJECT;
                        stateTimer.reset();
                    }
                    break;

                case PLACE_OBJECT:
                    // Lógica de colocación
                    currentState = State.PARK;
                    stateTimer.reset();
                    break;

                case PARK:
                    leftMotor.setPower(0.3);
                    rightMotor.setPower(0.3);

                    if (stateTimer.seconds() > 1.5) {
                        currentState = State.STOP;
                    }
                    break;
            }

            telemetry.addData("Estado Actual", currentState);
            telemetry.addData("Tiempo en Estado", stateTimer.seconds());
            telemetry.update();
        }

        // Detener todo
        leftMotor.setPower(0);
        rightMotor.setPower(0);
    }
}
```

## Odometría

### Odometría de 2 Ruedas

```java
public class Odometry {
    private double x = 0, y = 0, heading = 0;
    private double lastLeftEncoder = 0, lastRightEncoder = 0;

    private static final double WHEEL_DIAMETER = 2.0; // pulgadas
    private static final double TICKS_PER_REV = 8192;
    private static final double TRACK_WIDTH = 12.0; // pulgadas

    public void update(double leftEncoder, double rightEncoder, double imuHeading) {
        double leftDelta = (leftEncoder - lastLeftEncoder) / TICKS_PER_REV *
                          (Math.PI * WHEEL_DIAMETER);
        double rightDelta = (rightEncoder - lastRightEncoder) / TICKS_PER_REV *
                           (Math.PI * WHEEL_DIAMETER);

        double distance = (leftDelta + rightDelta) / 2.0;

        heading = Math.toRadians(imuHeading);

        x += distance * Math.cos(heading);
        y += distance * Math.sin(heading);

        lastLeftEncoder = leftEncoder;
        lastRightEncoder = rightEncoder;
    }

    public double getX() { return x; }
    public double getY() { return y; }
    public double getHeading() { return Math.toDegrees(heading); }
}
```

## Modos de Conducción (Drive Modes)

### Tank Drive

```java
double leftPower = -gamepad1.left_stick_y;
double rightPower = -gamepad1.right_stick_y;

leftMotor.setPower(leftPower);
rightMotor.setPower(rightPower);
```

### Arcade Drive

```java
double drive = -gamepad1.left_stick_y;  // Adelante/atrás
double turn = gamepad1.right_stick_x;   // Giro

double leftPower = drive + turn;
double rightPower = drive - turn;

leftMotor.setPower(Range.clip(leftPower, -1.0, 1.0));
rightMotor.setPower(Range.clip(rightPower, -1.0, 1.0));
```

### Mecanum Drive

```java
double y = -gamepad1.left_stick_y;  // Adelante/atrás
double x = gamepad1.left_stick_x;   // Izquierda/derecha
double turn = gamepad1.right_stick_x;

double frontLeftPower = y + x + turn;
double frontRightPower = y - x - turn;
double backLeftPower = y - x + turn;
double backRightPower = y + x - turn;

// Normalizar si algún valor excede 1.0
double max = Math.max(Math.abs(frontLeftPower), Math.max(Math.abs(frontRightPower),
              Math.max(Math.abs(backLeftPower), Math.abs(backRightPower))));
if (max > 1.0) {
    frontLeftPower /= max;
    frontRightPower /= max;
    backLeftPower /= max;
    backRightPower /= max;
}

frontLeft.setPower(frontLeftPower);
frontRight.setPower(frontRightPower);
backLeft.setPower(backLeftPower);
backRight.setPower(backRightPower);
```

### Field-Centric Drive (Mecanum)

```java
BNO055IMU imu = hardwareMap.get(BNO055IMU.class, "imu");
Orientation angles = imu.getAngularOrientation(...);
double heading = -Math.toRadians(angles.firstAngle);

double y = -gamepad1.left_stick_y;
double x = gamepad1.left_stick_x;
double turn = gamepad1.right_stick_x;

// Rotar vector de movimiento según orientación del robot
double rotX = x * Math.cos(heading) - y * Math.sin(heading);
double rotY = x * Math.sin(heading) + y * Math.cos(heading);

double frontLeftPower = rotY + rotX + turn;
double frontRightPower = rotY - rotX - turn;
double backLeftPower = rotY - rotX + turn;
double backRightPower = rotY + rotX - turn;

// Aplicar potencias...
```

## Programación Defensiva

### Try-Catch para Hardware

```java
DcMotor motor = null;

try {
    motor = hardwareMap.get(DcMotor.class, "motor");
} catch (Exception e) {
    telemetry.addData("ERROR", "Motor 'motor' no encontrado en configuración");
    telemetry.update();
}

if (motor != null) {
    motor.setPower(0.5);
}
```

### Verificar Null

```java
if (motor != null && motor.getCurrentPosition() > 100) {
    // Acción
}
```

### Limitar Valores

```java
import com.qualcomm.robotcore.util.Range;

double power = Range.clip(calculatedPower, -1.0, 1.0);
motor.setPower(power);
```

## Optimización de Performance

### Evitar Cálculos Innecesarios

```java
// MALO - calcula cada loop
while (opModeIsActive()) {
    double constant = Math.PI * 2.5 / 360.0; // ¡Siempre el mismo valor!
    double result = angle * constant;
}

// BUENO - calcula una vez
double constant = Math.PI * 2.5 / 360.0;
while (opModeIsActive()) {
    double result = angle * constant;
}
```

### Caché de Valores

```java
// MALO - lee encoder múltiples veces
if (motor.getCurrentPosition() > 100) {
    telemetry.addData("Pos", motor.getCurrentPosition());
    double velocity = motor.getCurrentPosition() - lastPosition;
}

// BUENO - lee una vez
int currentPosition = motor.getCurrentPosition();
if (currentPosition > 100) {
    telemetry.addData("Pos", currentPosition);
    double velocity = currentPosition - lastPosition;
}
```

### Limitar Frecuencia de Telemetría

```java
private int loopCount = 0;

while (opModeIsActive()) {
    // Tu código...

    // Actualizar telemetría cada 10 loops
    if (loopCount % 10 == 0) {
        telemetry.update();
    }
    loopCount++;
}
```

## Próximos Pasos

- [Sistema Eléctrico](../04_Sistema_Electrico/alimentacion.md) - Gestión de energía y cableado
- [FTCLib](../05_FTCLib/introduccion-ftclib.md) - Librerías avanzadas con PID integrado
- [Pedro Pathing](../07_Pedro_Pathing/introduccion-pedro.md) - Path following avanzado

---

**[← Anterior: Estructura OpMode](./estructura-opmode.md)** | **[→ Siguiente: Sistema Eléctrico](../04_Sistema_Electrico/alimentacion.md)** | **[↑ Índice](../INTRO_INDICE.md)**
