# Sensores en FTC

## Color Sensor (REV V3)

```java
ColorSensor colorSensor = hardwareMap.get(ColorSensor.class, "color");

int red = colorSensor.red();      // 0-255
int green = colorSensor.green();
int blue = colorSensor.blue();
int alpha = colorSensor.alpha();  // Intensidad total

// Distancia (si tiene sensor integrado)
DistanceSensor distanceSensor = (DistanceSensor) colorSensor;
double distance = distanceSensor.getDistance(DistanceUnit.CM);
```

## Distance Sensor (2m)

```java
DistanceSensor distanceSensor = hardwareMap.get(DistanceSensor.class, "distance");

double distanceCM = distanceSensor.getDistance(DistanceUnit.CM);
double distanceInch = distanceSensor.getDistance(DistanceUnit.INCH);
```

## IMU (BNO055)

```java
BNO055IMU imu = hardwareMap.get(BNO055IMU.class, "imu");

BNO055IMU.Parameters parameters = new BNO055IMU.Parameters();
parameters.angleUnit = BNO055IMU.AngleUnit.DEGREES;
imu.initialize(parameters);

// Leer orientación
Orientation angles = imu.getAngularOrientation(
    AxesReference.INTRINSIC, AxesOrder.ZYX, AngleUnit.DEGREES
);

double heading = angles.firstAngle;  // Yaw (-180 a 180)
double roll = angles.secondAngle;
double pitch = angles.thirdAngle;
```

## Touch Sensor

```java
DigitalChannel touchSensor = hardwareMap.get(DigitalChannel.class, "touch");
touchSensor.setMode(DigitalChannel.Mode.INPUT);

boolean isPressed = !touchSensor.getState();  // Active low
```

## Encoders Externos

```java
// Dead wheel odometry
DcMotor deadWheelLeft = hardwareMap.get(DcMotor.class, "odoLeft");
deadWheelLeft.setMode(DcMotor.RunMode.STOP_AND_RESET_ENCODER);
deadWheelLeft.setMode(DcMotor.RunMode.RUN_WITHOUT_ENCODER);

int position = deadWheelLeft.getCurrentPosition();
```

---

**[↑ Índice](../INTRO_INDICE.md)**
