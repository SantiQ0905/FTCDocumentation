# Servos en FTC

## Tipos de Servos

### Servo Estándar

- Rango: 0.0 (mínimo) a 1.0 (máximo)
- Rotación típica: 180° o 270°
- Uso: Posiciones fijas (garras, brazos)

```java
Servo servo = hardwareMap.get(Servo.class, "servo");
servo.setPosition(0.5);  // Centro
```

### Servo Continuo

- Rango: 0.0 (reversa) a 0.5 (stop) a 1.0 (adelante)
- Rotación continua
- Uso: Rodillos, intakes pequeños

```java
CRServo crServo = hardwareMap.get(CRServo.class, "crServo");
crServo.setPower(1.0);  // Rotación completa adelante
```

## Control de Servo

### Posiciones Predefinidas

```java
public class ClawServo {
    private Servo servo;
    private static final double OPEN = 0.5;
    private static final double CLOSED = 0.0;

    public ClawServo(Servo servo) {
        this.servo = servo;
    }

    public void open() {
        servo.setPosition(OPEN);
    }

    public void close() {
        servo.setPosition(CLOSED);
    }
}
```

### Movimiento Gradual

```java
public void moveToPosition(Servo servo, double targetPos, double step) {
    double currentPos = servo.getPosition();

    while (opModeIsActive() && Math.abs(targetPos - currentPos) > 0.01) {
        if (currentPos < targetPos) {
            currentPos += step;
        } else {
            currentPos -= step;
        }
        servo.setPosition(currentPos);
        sleep(20);
    }
}
```

## Gestión de Corriente

- Servos comparten 6A total
- Evitar mover múltiples servos pesados simultáneamente
- Monitorear caída de voltaje

---

**[↑ Índice](../INTRO_INDICE.md)**
