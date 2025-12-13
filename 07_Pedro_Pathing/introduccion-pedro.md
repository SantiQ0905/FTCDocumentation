# Pedro Pathing - Path Following Avanzado

## ¿Qué es Pedro Pathing?

**Pedro Pathing** es un sistema avanzado de seguimiento de trayectorias usando curvas de Bézier, desarrollado por FTC Team 10158. Ofrece movimiento suave, rápido y preciso para navegación autónoma.

## Características

- ✅ Curvas de Bézier para trayectorias suaves
- ✅ Control PIDF integrado
- ✅ Corrección de fuerza centrípeta
- ✅ Reactive path following
- ✅ Visualizador de trayectorias
- ✅ Más rápido y preciso que RoadRunner en muchos casos

## Instalación

```gradle
repositories {
    maven { url = 'https://jitpack.io' }
}

dependencies {
    implementation 'com.github.Pedro-Pathing:PedroPathing:v1.0.0'
}
```

## Configuración Básica

### 1. Configurar Follower

```java
import com.pedropathing.follower.Follower;
import com.pedropathing.localization.Pose;

Follower follower = new Follower(hardwareMap);

// Configurar encoders de odometría
follower.setStartingPose(new Pose(0, 0, 0));
```

### 2. Crear Path

```java
import com.pedropathing.pathgen.BezierCurve;
import com.pedropathing.pathgen.Path;
import com.pedropathing.pathgen.Point;

// Path simple de A a B
Path path = new Path(new BezierCurve(
    new Point(0, 0, Point.CARTESIAN),
    new Point(48, 48, Point.CARTESIAN)
));

follower.followPath(path);
```

### 3. Update Loop

```java
@Override
public void runOpMode() {
    follower = new Follower(hardwareMap);
    follower.setStartingPose(new Pose(0, 0, 0));

    // Crear path
    Path path = new Path(...);
    follower.followPath(path);

    waitForStart();

    while (opModeIsActive()) {
        follower.update();  // IMPORTANTE: Llamar cada loop

        Pose currentPose = follower.getPose();
        telemetry.addData("X", currentPose.getX());
        telemetry.addData("Y", currentPose.getY());
        telemetry.addData("Heading", currentPose.getHeading());
        telemetry.update();
    }
}
```

## Path Types

### Bezier Curve (Suave)

```java
Path smoothPath = new Path(new BezierCurve(
    new Point(0, 0, Point.CARTESIAN),
    new Point(24, 12, Point.CARTESIAN),  // Control point
    new Point(48, 0, Point.CARTESIAN)
));
```

### Bezier Line (Línea recta)

```java
Path straightPath = new Path(new BezierLine(
    new Point(0, 0, Point.CARTESIAN),
    new Point(48, 48, Point.CARTESIAN)
));
```

## Path Actions

### Heading Interpolation

```java
path.setLinearHeadingInterpolation(0, Math.toRadians(90));
```

### Velocidad Variable

```java
path.setPathEndVelocityConstraint(0);  // Detener al final
```

## Ejemplo Completo - Autonomous

```java
@Autonomous(name="Pedro Auto", group="Auto")
public class PedroAuto extends LinearOpMode {

    private Follower follower;

    @Override
    public void runOpMode() {
        follower = new Follower(hardwareMap);
        follower.setStartingPose(new Pose(0, 0, 0));

        // Path 1: Mover adelante
        Path path1 = new Path(new BezierLine(
            new Point(0, 0, Point.CARTESIAN),
            new Point(48, 0, Point.CARTESIAN)
        ));
        path1.setLinearHeadingInterpolation(0, 0);

        // Path 2: Girar y mover
        Path path2 = new Path(new BezierCurve(
            new Point(48, 0, Point.CARTESIAN),
            new Point(48, 24, Point.CARTESIAN),
            new Point(24, 48, Point.CARTESIAN)
        ));
        path2.setLinearHeadingInterpolation(0, Math.toRadians(90));

        waitForStart();

        // Ejecutar path 1
        follower.followPath(path1);
        while (opModeIsActive() && follower.isBusy()) {
            follower.update();
            telemetry.addData("Status", "Path 1");
            telemetry.update();
        }

        // Ejecutar path 2
        follower.followPath(path2);
        while (opModeIsActive() && follower.isBusy()) {
            follower.update();
            telemetry.addData("Status", "Path 2");
            telemetry.update();
        }
    }
}
```

## Tuning

### Constantes de Follower

En `Follower.java` o mediante configuración:

```java
// PIDF para translación
follower.setTranslationalPIDFCoefficients(0.1, 0.0, 0.01, 0.0);

// PIDF para heading
follower.setHeadingPIDFCoefficients(2.0, 0.0, 0.1, 0.0);

// Fuerza centrípeta
follower.setCentripetal(0.0001);
```

## Visualizador

Pedro Pathing incluye visualizador para diseñar paths:

1. Visita https://pedropathing.com/visualizer
2. Diseña tu path visualmente
3. Copia código generado a tu OpMode

## Comparación con RoadRunner

| Característica | Pedro Pathing | RoadRunner |
|----------------|---------------|------------|
| Curvas | Bézier | Splines |
| Velocidad | Más rápido | Estándar |
| Facilidad | Más simple | Más complejo |
| Tuning | Menos parámetros | Muchos parámetros |
| Comunidad | Creciente | Establecida |

## Recursos

- **Documentación**: https://pedropathing.com/docs
- **Visualizador**: https://pedropathing.com/visualizer
- **GitHub**: https://github.com/Pedro-Pathing
- **Tutoriales**: Canal YouTube de Team 10158

---

**[↑ Índice](../INTRO_INDICE.md)**
