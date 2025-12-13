# Utilidades FTCLib

## Timing

```java
import com.arcrobotics.ftclib.util.Timing.Timer;

Timer timer = new Timer(3000);  // 3 segundos
timer.start();

if (timer.done()) {
    // Acción después de 3s
}
```

## Range Clipping

```java
import com.arcrobotics.ftclib.util.MathUtils;

double clipped = MathUtils.clamp(value, -1.0, 1.0);
```

---

**[↑ Índice](../INTRO_INDICE.md)**
