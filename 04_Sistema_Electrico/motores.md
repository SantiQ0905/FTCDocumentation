# Motores DC en FTC

## Motores Comunes

### REV HD Hex Motor

- Velocidad libre: 6000 RPM
- Torque: 3.2 N·m
- Encoder: 28 PPR
- Uso: Drivetrain alta velocidad con reducción externa

### REV Core Hex

- Velocidad: 125 RPM (reducción 72:1 integrada)
- Torque: 1.9 N·m
- Encoder integrado
- Uso: Mecanismos de torque

### goBILDA Yellow Jacket

- Múltiples relaciones: 5.2 a 1620
- Encoder integrado
- Versatilidad para diferentes aplicaciones

## Cálculos de Encoder

```java
// Constantes
static final double COUNTS_PER_MOTOR_REV = 28;  // HD Hex sin reducción
static final double DRIVE_GEAR_REDUCTION = 20.0; // Reducción externa
static final double WHEEL_DIAMETER_INCHES = 4.0;

static final double COUNTS_PER_INCH =
    (COUNTS_PER_MOTOR_REV * DRIVE_GEAR_REDUCTION) /
    (WHEEL_DIAMETER_INCHES * Math.PI);

// Uso
int targetPosition = (int)(distanceInches * COUNTS_PER_INCH);
motor.setTargetPosition(targetPosition);
```

## Modos de Control

### RUN_WITHOUT_ENCODER

```java
motor.setMode(DcMotor.RunMode.RUN_WITHOUT_ENCODER);
motor.setPower(0.5);  // Potencia directa, sin feedback
```

### RUN_USING_ENCODER

```java
motor.setMode(DcMotor.RunMode.RUN_USING_ENCODER);
motor.setPower(0.5);  // Control velocidad con PID interno
```

### RUN_TO_POSITION

```java
motor.setTargetPosition(1000);
motor.setMode(DcMotor.RunMode.RUN_TO_POSITION);
motor.setPower(0.5);

while (motor.isBusy()) {
    // Espera
}
motor.setPower(0);
```

## ZeroPowerBehavior

```java
// BRAKE: Frena activamente
motor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.BRAKE);

// FLOAT: Rueda libremente
motor.setZeroPowerBehavior(DcMotor.ZeroPowerBehavior.FLOAT);
```

---

**[↑ Índice](../INTRO_INDICE.md)**
