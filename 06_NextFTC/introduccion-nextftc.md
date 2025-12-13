# NextFTC - Framework Moderno para FTC

## ¿Qué es NextFTC?

**NextFTC** es un framework command-based moderno y simple para FTC. Incluye integración con Pedro Pathing y FTC Dashboard.

## Instalación

```gradle
repositories {
    maven { url = 'https://jitpack.io' }
}

dependencies {
    implementation 'com.github.NextFTC:NextFTC:0.6.1'
    // Incluye automáticamente PedroPathing y FTC Dashboard
}
```

## Estructura

### Comandos

```java
import org.nextftc.nextftc.command.Command;

public class MoveForward extends Command {
    private DcMotor motor;

    public MoveForward(DcMotor motor) {
        this.motor = motor;
    }

    @Override
    public void execute() {
        motor.setPower(0.5);
    }

    @Override
    public boolean isFinished() {
        return motor.getCurrentPosition() > 1000;
    }

    @Override
    public void end() {
        motor.setPower(0);
    }
}
```

### Subsistemas

```java
import org.nextftc.nextftc.subsystem.Subsystem;

public class Drivetrain extends Subsystem {
    private DcMotor left, right;

    public Drivetrain(DcMotor left, DcMotor right) {
        this.left = left;
        this.right = right;
    }

    public void drive(double leftPower, double rightPower) {
        left.setPower(leftPower);
        right.setPower(rightPower);
    }
}
```

## Recursos

- **Documentación**: https://nextftc.dev
- **GitHub**: https://github.com/NextFTC/NextFTC
- **Discord**: Comunidad activa

---

**[↑ Índice](../INTRO_INDICE.md)**
