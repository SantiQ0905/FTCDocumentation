# Controladores en FTCLib

## PID Controller

```java
PIDController pid = new PIDController(kp, ki, kd);
pid.setSetPoint(targetPosition);

double output = pid.calculate(currentPosition);
motor.set(output);
```

## PID con Feedforward

```java
PIDFController pidf = new PIDFController(kp, ki, kd, kf);
```

---

**[↑ Índice](../INTRO_INDICE.md)**
