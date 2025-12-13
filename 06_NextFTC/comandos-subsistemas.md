# Comandos y Subsistemas en NextFTC

## Comandos Secuenciales

```java
Command sequence = new SequentialCommandGroup(
    new MoveForward(motor),
    new TurnRight(motor),
    new PlaceObject(servo)
);
```

## Comandos Paralelos

```java
Command parallel = new ParallelCommandGroup(
    new DriveForward(drivetrain),
    new RaiseArm(armMotor)
);
```

---

**[↑ Índice](../INTRO_INDICE.md)**
