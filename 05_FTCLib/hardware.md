# Hardware en FTCLib

## Motor Groups

```java
import com.arcrobotics.ftclib.hardware.motors.MotorGroup;

Motor left1 = new Motor(hardwareMap, "left1");
Motor left2 = new Motor(hardwareMap, "left2");

MotorGroup leftGroup = new MotorGroup(left1, left2);
leftGroup.set(0.5);  // Ambos motores a 50%
```

## Sensores

### Distance Sensor

```java
import com.arcrobotics.ftclib.hardware.GyroEx;

GyroEx gyro = new GyroEx(hardwareMap, "imu");
double heading = gyro.getHeading();
```

---

**[↑ Índice](../INTRO_INDICE.md)**
