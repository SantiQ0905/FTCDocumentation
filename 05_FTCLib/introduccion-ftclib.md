# FTCLib - Librería Avanzada para FTC

## ¿Qué es FTCLib?

**FTCLib** es una librería completa para FTC que proporciona implementaciones robustas de algoritmos comunes, command-based programming, y utilidades avanzadas. Inspirada en WPILib de FRC.

## Instalación

### build.gradle (TeamCode)

```gradle
dependencies {
    implementation 'org.ftclib.ftclib:core:2.1.1'
}
```

Después: Click "Sync Now"

## Características Principales

### 1. Hardware Wrappers

#### Motor con FTCLib

```java
import com.arcrobotics.ftclib.hardware.motors.Motor;
import com.arcrobotics.ftclib.hardware.motors.MotorEx;

// Motor básico
Motor motor = new Motor(hardwareMap, "motor");
motor.set(0.5);  // Potencia

// Motor extendido con encoder
MotorEx motorEx = new MotorEx(hardwareMap, "motorEx");
motorEx.setRunMode(Motor.RunMode.PositionControl);
motorEx.setTargetPosition(1000);
motorEx.set(0.5);
```

#### Servo con FTCLib

```java
import com.arcrobotics.ftclib.hardware.SimpleServo;

SimpleServo servo = new SimpleServo(hardwareMap, "servo", 0, 180);
servo.setPosition(0.5);  // 0-1
servo.turnToAngle(90);   // Grados
```

### 2. PID Controller

```java
import com.arcrobotics.ftclib.controller.PIDController;

PIDController pid = new PIDController(0.01, 0, 0.001);

while (opModeIsActive()) {
    double output = pid.calculate(motor.getCurrentPosition(), targetPosition);
    motor.set(output);

    telemetry.addData("Error", pid.getPositionError());
    telemetry.update();
}
```

### 3. Drivetrain Classes

#### Mecanum Drive

```java
import com.arcrobotics.ftclib.drivebase.MecanumDrive;
import com.arcrobotics.ftclib.hardware.motors.Motor;

Motor frontLeft = new Motor(hardwareMap, "frontLeft");
Motor frontRight = new Motor(hardwareMap, "frontRight");
Motor backLeft = new Motor(hardwareMap, "backLeft");
Motor backRight = new Motor(hardwareMap, "backRight");

MecanumDrive drive = new MecanumDrive(frontLeft, frontRight, backLeft, backRight);

// En loop
drive.driveRobotCentric(
    -gamepad1.left_stick_x,
    -gamepad1.left_stick_y,
    -gamepad1.right_stick_x
);
```

#### Field-Centric

```java
import com.arcrobotics.ftclib.hardware.RevIMU;

RevIMU imu = new RevIMU(hardwareMap);
imu.init();

// En loop
drive.driveFieldCentric(
    -gamepad1.left_stick_x,
    -gamepad1.left_stick_y,
    -gamepad1.right_stick_x,
    imu.getHeading()
);
```

### 4. Command-Based Programming

#### Command Example

```java
import com.arcrobotics.ftclib.command.CommandOpMode;
import com.arcrobotics.ftclib.command.InstantCommand;
import com.arcrobotics.ftclib.command.button.GamepadButton;
import com.arcrobotics.ftclib.gamepad.GamepadEx;
import com.arcrobotics.ftclib.gamepad.GamepadKeys;

@TeleOp
public class CommandOpModeExample extends CommandOpMode {

    @Override
    public void initialize() {
        GamepadEx driverOp = new GamepadEx(gamepad1);

        // Botón A abre garra
        driverOp.getGamepadButton(GamepadKeys.Button.A)
            .whenPressed(new InstantCommand(() -> {
                clawServo.setPosition(0.5);
            }));

        // Botón B cierra garra
        driverOp.getGamepadButton(GamepadKeys.Button.B)
            .whenPressed(new InstantCommand(() -> {
                clawServo.setPosition(0.0);
            }));
    }
}
```

### 5. Odometry

```java
import com.arcrobotics.ftclib.kinematics.HolonomicOdometry;

HolonomicOdometry odometry = new HolonomicOdometry(
    () -> leftEncoder.getDistance(),
    () -> rightEncoder.getDistance(),
    () -> frontEncoder.getDistance(),
    TRACKWIDTH,
    CENTER_WHEEL_OFFSET
);

// En loop
odometry.updatePose();

double x = odometry.getPose().getX();
double y = odometry.getPose().getY();
double heading = odometry.getPose().getHeading();
```

## Recursos

- **Documentación**: https://docs.ftclib.org/
- **GitHub**: https://github.com/FTCLib/FTCLib
- **Discord**: Comunidad activa para soporte

---

**[↑ Índice](../INTRO_INDICE.md)**
