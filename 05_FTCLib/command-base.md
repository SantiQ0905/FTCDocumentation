# Command-Based Programming - FTCLib

## Conceptos

**Subsystems**: Representan componentes del robot (drivetrain, intake, etc.)
**Commands**: Acciones que operan sobre subsystems
**Scheduler**: Gestiona ejecución de commands

## Ejemplo Subsystem

```java
import com.arcrobotics.ftclib.command.SubsystemBase;

public class DriveSubsystem extends SubsystemBase {
    private Motor left, right;

    public DriveSubsystem(Motor left, Motor right) {
        this.left = left;
        this.right = right;
    }

    public void drive(double leftPower, double rightPower) {
        left.set(leftPower);
        right.set(rightPower);
    }

    public void stop() {
        drive(0, 0);
    }
}
```

## Ejemplo Command

```java
import com.arcrobotics.ftclib.command.CommandBase;

public class DriveCommand extends CommandBase {
    private DriveSubsystem drive;
    private DoubleSupplier leftPower, rightPower;

    public DriveCommand(DriveSubsystem drive, DoubleSupplier left, DoubleSupplier right) {
        this.drive = drive;
        this.leftPower = left;
        this.rightPower = right;
        addRequirements(drive);
    }

    @Override
    public void execute() {
        drive.drive(leftPower.getAsDouble(), rightPower.getAsDouble());
    }
}
```

---

**[↑ Índice](../INTRO_INDICE.md)**
