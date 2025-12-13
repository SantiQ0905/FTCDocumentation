# FTC Dashboard - Telemetría Avanzada

## ¿Qué es FTC Dashboard?

Herramienta web para visualizar telemetría en tiempo real, configurar variables, y graficar datos.

## Instalación

```gradle
dependencies {
    implementation 'com.acmerobotics.dashboard:dashboard:0.4.12'
}
```

## Uso Básico

```java
import com.acmerobotics.dashboard.FtcDashboard;
import com.acmerobotics.dashboard.telemetry.TelemetryPacket;

FtcDashboard dashboard = FtcDashboard.getInstance();

// En loop
TelemetryPacket packet = new TelemetryPacket();
packet.put("x", robotX);
packet.put("y", robotY);
packet.put("heading", robotHeading);

dashboard.sendTelemetryPacket(packet);
```

## Acceso

1. Conecta al Wi-Fi del Control Hub
2. Navega a: `http://192.168.43.1:8080/dash`

## Características

- 📊 Gráficos en tiempo real
- 🎛️ Configuración de variables en vivo
- 🗺️ Visualización de trayectorias
- 📷 Stream de cámara

---

**[↑ Índice](../INTRO_INDICE.md)**
