# Configuración de Pedro Pathing

## Configurar Encoders de Odometría

```java
follower.setEncoders(
    leftEncoder,
    rightEncoder,
    frontEncoder
);
```

## Constantes del Robot

```java
public class DriveConstants {
    public static double TRACK_WIDTH = 12.0;  // Pulgadas
    public static double CENTER_WHEEL_OFFSET = 6.0;
    public static double WHEEL_DIAMETER = 2.0;
    public static double TICKS_PER_REV = 8192;
}
```

## Tuning PID

```java
// Empezar con valores conservadores
follower.setTranslationalPIDFCoefficients(0.05, 0.0, 0.005, 0.0);
follower.setHeadingPIDFCoefficients(1.0, 0.0, 0.05, 0.0);

// Ajustar hasta movimiento suave sin oscilaciones
```

---

**[↑ Índice](../INTRO_INDICE.md)**
