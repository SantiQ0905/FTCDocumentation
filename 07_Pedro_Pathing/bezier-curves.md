# Curvas de Bézier en Pedro Pathing

## ¿Qué son las Curvas de Bézier?

Curvas matemáticas suaves definidas por puntos de control. Permiten trayectorias más naturales que líneas rectas.

## Tipos de Curvas

### Línea Bézier (2 puntos)

```java
BezierLine line = new BezierLine(
    new Point(0, 0, Point.CARTESIAN),
    new Point(48, 48, Point.CARTESIAN)
);
```

### Curva Bézier Cuadrática (3 puntos)

```java
BezierCurve curve = new BezierCurve(
    new Point(0, 0, Point.CARTESIAN),      // Start
    new Point(24, 24, Point.CARTESIAN),    // Control point
    new Point(48, 0, Point.CARTESIAN)      // End
);
```

### Curva Bézier Cúbica (4 puntos)

```java
BezierCurve cubic = new BezierCurve(
    new Point(0, 0, Point.CARTESIAN),
    new Point(16, 16, Point.CARTESIAN),
    new Point(32, 16, Point.CARTESIAN),
    new Point(48, 0, Point.CARTESIAN)
);
```

---

**[↑ Índice](../INTRO_INDICE.md)**
