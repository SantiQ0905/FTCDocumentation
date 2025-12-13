# Driver Station - Interfaz de Control del Robot

## Introducción

La **Driver Station (DS)** es la aplicación Android que sirve como interfaz entre los conductores y el robot. Permite iniciar/detener OpModes, conectar gamepads, monitorear telemetría y diagnosticar problemas en tiempo real.

## Requisitos del Dispositivo

### Hardware Mínimo

- **Sistema Operativo**: Android 6.0 (Marshmallow) o superior
  - Recomendado: Android 8.0+
- **Procesador**: Quad-core 1.5 GHz mínimo
- **RAM**: 2 GB mínimo (4 GB recomendado)
- **Pantalla**: 5" mínimo (7"-10" recomendado para visibilidad)
- **Conectividad**: Wi-Fi 2.4GHz y 5GHz
- **Puertos USB**: Al menos 1 (para gamepads cableados)
- **Bluetooth**: 4.0+ (para gamepads inalámbricos)

### Dispositivos Recomendados

**Teléfonos**:
- Motorola Moto G series
- Samsung Galaxy A series
- Google Pixel (cualquier generación)

**Tablets** (mejor visibilidad):
- Samsung Galaxy Tab A
- Amazon Fire HD 8/10
- Lenovo Tab M series

### Instalación de la App

#### Método 1: Google Play Store

1. Abre Google Play Store
2. Busca "FTC Driver Station"
3. Instala la app oficial de *FIRST*
4. Abre y concede permisos necesarios

#### Método 2: APK Manual (Para dispositivos sin Play Store)

1. Descarga el APK desde [GitHub FIRST Tech Challenge](https://github.com/FIRST-Tech-Challenge/FtcRobotController/releases)
2. Archivo: `FtcDriverStation-release.apk`
3. Habilita "Instalar apps desconocidas" en configuración de Android
4. Instala el APK
5. Abre la aplicación

## Interfaz de Usuario

### Pantalla Principal

```
┌─────────────────────────────────────────────┐
│  FTC Driver Station            [⋮] [●] [i] │
├─────────────────────────────────────────────┤
│                                             │
│  ●  FTC-AB12                     12.4V  ▲  │
│     Connected                              │
│                                             │
├─────────────────────────────────────────────┤
│  Select OpMode ▼                           │
│  ┌─────────────────────────────────────┐   │
│  │  TeleOp: MiOpMode                   │   │
│  │  Autonomous: AutonomoRojo           │   │
│  │  Autonomous: AutonomoAzul           │   │
│  └─────────────────────────────────────┘   │
│                                             │
│  [   INIT   ]  [  START  ]  [  STOP  ]    │
│                                             │
├─────────────────────────────────────────────┤
│  Telemetría:                               │
│  Status: Initialized                       │
│  Left Power: 0.00                          │
│  Right Power: 0.00                         │
│                                             │
├─────────────────────────────────────────────┤
│  🎮 Gamepad 1: Logitech F310 (USB)        │
│  🎮 Gamepad 2: No conectado               │
└─────────────────────────────────────────────┘
```

### Elementos de la Interfaz

#### Indicador de Conexión (Superior)

- **Círculo Verde (●)**: Conectado al Control Hub
- **Círculo Rojo (●)**: Desconectado
- **Nombre del Robot**: "FTC-XXXX" o nombre personalizado
- **Voltaje de Batería**: Actualizado en tiempo real
  - Verde: >12.5V
  - Amarillo: 11.5V - 12.5V
  - Rojo: <11.5V (¡Cambia batería!)

#### Selector de OpMode

Menú desplegable que lista todos los OpModes disponibles:
- **TeleOp**: OpModes controlados por humano
- **Autonomous**: OpModes autónomos
- Organizados alfabéticamente dentro de cada categoría

#### Botones de Control

**INIT**:
- Inicializa el OpMode seleccionado
- Ejecuta código de inicialización (antes de `waitForStart()`)
- Útil para verificar que todo funciona antes de iniciar

**START** (▶):
- Inicia la ejecución del OpMode
- Solo disponible después de INIT
- Comienza el bucle principal del OpMode

**STOP** (⏹):
- Detiene el OpMode inmediatamente
- Motores se ponen a potencia 0
- Libera recursos

#### Panel de Telemetría

Muestra información enviada desde el OpMode:
```java
telemetry.addData("Estado", "Moviendo hacia adelante");
telemetry.addData("Distancia", "%.2f cm", distancia);
telemetry.update();
```

Aparece en la Driver Station en tiempo real.

#### Indicadores de Gamepad

Muestra gamepads conectados:
- **Gamepad 1**: Principal (conductor)
- **Gamepad 2**: Secundario (operador de mecanismos)
- Tipo de conexión: USB, Bluetooth
- Modelo del gamepad

## Configuración

### Conectar al Control Hub

#### Wi-Fi Direct

1. En el dispositivo de la Driver Station, abre **Configuración de Wi-Fi**
2. Busca la red `FTC-XXXX` (XXXX = últimos 4 dígitos del número de serie)
3. Conecta usando la contraseña del Control Hub
   - Por defecto: ver etiqueta del Control Hub
   - Común: `password`
4. Abre la app Driver Station
5. Debe conectarse automáticamente

#### Emparejamiento de Control Hub

Si no conecta automáticamente:

1. En Driver Station, toca el menú (⋮) → **Settings**
2. **Pairing Method**: "Wi-Fi Direct"
3. **Choose Robot Controller**: Selecciona "FTC-XXXX"
4. Toca "Connect"

### Conectar Gamepads

#### Gamepad USB

1. Conecta el gamepad al puerto USB del dispositivo Driver Station
2. El dispositivo debe reconocerlo automáticamente
3. Aparecerá en la Driver Station como "Gamepad 1" o "Gamepad 2"

#### Gamepad Bluetooth

**Paso 1: Emparejar con Android**

1. Coloca el gamepad en modo de emparejamiento:
   - **Xbox**: Mantén botón de emparejamiento
   - **PS4**: Mantén Share + PS simultáneamente
   - **Otros**: Consulta manual
2. En Android: Configuración → Bluetooth
3. Busca dispositivos → Selecciona tu gamepad
4. Empareja

**Paso 2: Asignar en Driver Station**

1. En Driver Station, toca el menú (⋮) → **Settings**
2. **Gamepad Configuration**
3. Asigna el gamepad emparejado como "Gamepad 1" o "Gamepad 2"

#### Tipos de Gamepad Compatibles

- **Logitech F310**: USB, muy popular en FTC
- **Xbox 360 Controller**: USB o Wireless (con dongle)
- **Xbox One Controller**: Bluetooth o USB-C
- **PS4 DualShock 4**: Bluetooth o USB
- **Etpark/Otros genéricos**: Verificar compatibilidad

### Configurar OpMode

#### Ordenar OpModes

Los OpModes aparecen ordenados por:
1. Tipo (Autonomous, TeleOp)
2. Grupo (si se especifica en `@TeleOp(group="...")`)
3. Nombre alfabéticamente

#### Ocultar OpModes en Competencia

En el código, usa `@Disabled` para ocultar OpModes:

```java
@Disabled
@TeleOp(name="OpMode En Desarrollo", group="Testing")
public class DevOpMode extends LinearOpMode {
    // Este OpMode no aparecerá en la lista
}
```

## Uso Durante Competencias

### Pre-Match

1. **Verificar Conexión**:
   - Driver Station conectada al Control Hub
   - Indicador verde, voltaje >12V

2. **Verificar Gamepads**:
   - Ambos gamepads conectados y detectados
   - Botones responden (presiona y observa feedback visual)

3. **Seleccionar OpMode**:
   - Para Autonomous: Selecciona el OpMode apropiado (rojo/azul, lado correcto)
   - Para TeleOp: Selecciona tu OpMode principal

### Durante Autonomous (30 segundos)

1. **Antes del inicio**:
   - Referee verifica que el OpMode esté seleccionado
   - **No presiones INIT hasta que el referee lo indique**

2. **Cuando el referee indica**:
   - Presiona **INIT**
   - Verifica mensaje de telemetría "Initialized" o similar
   - **Espera** a que el referee diga "START"

3. **Al inicio del partido**:
   - Presiona **START** (▶)
   - No toques el gamepad durante autónomo (puede descalificar)
   - Observa telemetría para monitorear progreso

4. **Si hay problemas**:
   - Presiona **STOP** solo en emergencia grave
   - Detenerse prematuramente puede costar puntos

### Durante TeleOp (2 minutos)

1. **Transición de Autónomo a TeleOp**:
   - El OpMode autónomo termina automáticamente a los 30 segundos
   - Presiona **STOP** si no se detuvo
   - Selecciona OpMode de TeleOp
   - Presiona **INIT** → **START**

2. **Durante operación**:
   - Los conductores usan los gamepads
   - Monitorea voltaje de batería
   - Observa telemetría para diagnóstico

3. **Al finalizar**:
   - El OpMode se detiene automáticamente después de 2:30 total
   - O presiona **STOP** al finalizar

### End Game (últimos 30 segundos)

- Muchos equipos usan telemetría para mostrar un temporizador
- Alerts de audio/visuales cuando quedan 30s, 10s, etc.

```java
double timeRemaining = 150 - runtime.seconds(); // 2:30 = 150s
if (timeRemaining <= 30 && timeRemaining > 29) {
    telemetry.addData("ALERT", "ENDGAME!");
}
```

## Telemetría Avanzada

### Formato de Telemetría

```java
// Texto simple
telemetry.addData("Estado", "Listo");

// Con formato
telemetry.addData("Voltaje", "%.2f V", batteryVoltage);

// Múltiples valores
telemetry.addData("Posición", "X: %.1f, Y: %.1f", x, y);

// Líneas largas
telemetry.addLine("Esta es una línea de telemetría larga que no tiene clave");

// Actualizar pantalla
telemetry.update();
```

### Organización de Telemetría

```java
telemetry.addLine("=== DRIVETRAIN ===");
telemetry.addData("Left Power", leftPower);
telemetry.addData("Right Power", rightPower);

telemetry.addLine();
telemetry.addLine("=== MECANISMOS ===");
telemetry.addData("Arm Position", armPosition);
telemetry.addData("Claw", clawOpen ? "Abierto" : "Cerrado");

telemetry.addLine();
telemetry.addData("Batería", "%.1f V", voltage);
telemetry.addData("Loop Time", "%.1f ms", loopTime);

telemetry.update();
```

### Telemetría Condicional

```java
// Solo mostrar advertencias si hay problemas
if (voltage < 12.0) {
    telemetry.addData("ADVERTENCIA", "Batería Baja!");
}

if (!imu.isGyroCalibrated()) {
    telemetry.addData("ADVERTENCIA", "IMU no calibrada");
}

telemetry.update();
```

### Limitar Frecuencia de Actualización

```java
// Actualizar telemetría solo cada 100ms para mejor rendimiento
private ElapsedTime telemetryTimer = new ElapsedTime();

public void updateTelemetry() {
    if (telemetryTimer.milliseconds() > 100) {
        telemetry.addData("Status", "Running");
        telemetry.update();
        telemetryTimer.reset();
    }
}
```

## Configuración Avanzada

### Settings (Configuración)

Acceso: Menú (⋮) → Settings

#### Advanced Settings

- **Pair with Robot Controller**: Emparejamiento manual
- **Connection Type**: Wi-Fi Direct (por defecto)
- **Robot Controller Address**: IP del Control Hub (192.168.43.1 por defecto)

#### Gamepad Configuration

- **Gamepad Type**: Detección automática o manual
- **Button Mapping**: Configuración de botones (raramente necesario)

#### App Settings

- **Keep Screen On**: Mantener pantalla encendida (recomendado: ON)
- **Sound Effects**: Efectos de sonido (recomendado: ON para alertas)
- **Haptic Feedback**: Vibración al presionar botones

### Modo de Competencia

Algunas competencias usan **Match Controller** que:
- Controla cuándo puedes presionar INIT/START
- Sincroniza temporizadores entre campos
- No disponible en práctica normal

## Troubleshooting

### No Conecta al Control Hub

**Síntomas**: Círculo rojo, "Not Connected"

**Soluciones**:
1. Verifica que el Control Hub esté encendido (LED verde)
2. Verifica conexión Wi-Fi del dispositivo al "FTC-XXXX"
3. Olvida la red Wi-Fi y reconecta
4. Reinicia la app Driver Station
5. Reinicia el Control Hub
6. Verifica que estés usando la contraseña correcta

### Gamepad No Detectado

**Síntomas**: "No gamepad detected" o no responde

**Soluciones USB**:
1. Desconecta y reconecta el cable USB
2. Prueba otro puerto USB (si el dispositivo tiene múltiples)
3. Prueba otro cable USB
4. Verifica que el gamepad funcione en otro dispositivo

**Soluciones Bluetooth**:
1. Verifica emparejamiento en Android Settings → Bluetooth
2. Desempareja y vuelve a emparejar
3. Reinicia el gamepad (apaga/enciende)
4. Reinicia Bluetooth en el dispositivo Android
5. En Driver Station Settings → Gamepad Config, reasigna el gamepad

### Telemetría No Aparece

**Síntomas**: Panel de telemetría vacío o no actualiza

**Verificar en el código**:
```java
// Asegúrate de llamar update()
telemetry.addData("Test", "Hola");
telemetry.update();  // ← IMPORTANTE
```

**Otras causas**:
- El OpMode no está en ejecución (presiona INIT → START)
- El OpMode tiene un error y se detuvo
- La sección de código con telemetría nunca se ejecuta

### Lag o Retraso en Controles

**Síntomas**: El robot responde con retraso a comandos del gamepad

**Causas y Soluciones**:

1. **Código bloqueado en el OpMode**:
```java
// MALO: Bloquea el bucle
while (someCondition) {
    // Código que toma mucho tiempo
}

// BUENO: Chequeo rápido en cada iteración
if (someCondition) {
    // Acción rápida
}
```

2. **Sleeps largos**:
```java
// MALO en TeleOp
sleep(1000);  // 1 segundo sin respuesta

// BUENO: Usar temporizadores
ElapsedTime timer = new ElapsedTime();
if (timer.seconds() > 1.0) {
    // Hacer acción
    timer.reset();
}
```

3. **Wi-Fi congestionado**:
   - Cambia canal Wi-Fi en configuración del Control Hub
   - Reduce interferencia de otros dispositivos

### Voltaje de Batería Incorrecto

**Síntomas**: Voltaje mostrado no coincide con multímetro

**Soluciones**:
1. El voltaje bajo carga es diferente al sin carga (normal)
2. Cables flojos pueden causar caídas de voltaje
3. Verifica conexiones XT30
4. Si el problema persiste, puede ser sensor de voltaje defectuoso

## Mejores Prácticas

### Para Conductores

1. **Familiarízate con la interfaz** antes de la competencia
2. **Practica** la transición Autónomo → TeleOp rápidamente
3. **Comunica** con tu compañero sobre el gamepad (quién es 1, quién es 2)
4. **Observa el voltaje** y avisa cuando esté bajo
5. **No toques** START hasta que el referee lo indique

### Para Programadores

1. **Telemetría útil**: Muestra información relevante, no excesiva
2. **Mensajes claros**: "Arm: UP" es mejor que "ArmPos: 1"
3. **Alertas visuales**: Usa mayúsculas para advertencias
4. **Organiza** la telemetría en secciones
5. **Prueba** toda la telemetría antes de competencia

### Para el Equipo

1. **Lleva backup** del dispositivo Driver Station
2. **Carga completa** antes de cada competencia
3. **Lleva cables USB de repuesto** para gamepads
4. **Protector de pantalla y case** para el dispositivo
5. **Documenta** configuraciones y contraseñas

## FTC Dashboard (Herramienta Adicional)

### ¿Qué es FTC Dashboard?

Una herramienta avanzada que proporciona:
- Interfaz web en tiempo real
- Gráficos de telemetría
- Configuración de variables en tiempo real
- Visualización de trayectorias

### Instalación

```gradle
// En build.gradle del módulo TeamCode
dependencies {
    implementation 'com.acmerobotics.dashboard:dashboard:0.4.12'
}
```

### Acceso

1. Conecta al Wi-Fi del Control Hub
2. Abre navegador: `http://192.168.43.1:8080/dash`
3. Interfaz gráfica con telemetría en vivo

### Uso Básico

```java
import com.acmerobotics.dashboard.FtcDashboard;
import com.acmerobotics.dashboard.telemetry.TelemetryPacket;

FtcDashboard dashboard = FtcDashboard.getInstance();
TelemetryPacket packet = new TelemetryPacket();

packet.put("x", robotX);
packet.put("y", robotY);
packet.put("heading", robotHeading);

dashboard.sendTelemetryPacket(packet);
```

**Ventajas sobre telemetría estándar**:
- Gráficos en tiempo real
- Persistencia de datos (no desaparece)
- Acceso desde laptop (mejor para debugging)

## Próximos Pasos

- [Comunicaciones](./comunicaciones.md) - Optimizar conexión Wi-Fi
- [Programación](../03_Programacion/estructura-opmode.md) - Crear OpModes efectivos
- [Telemetría Avanzada](../03_Programacion/conceptos-basicos.md) - Debugging y monitoreo

---

**[← Anterior: Expansion Hub](./expansion-hub.md)** | **[→ Siguiente: Comunicaciones](./comunicaciones.md)** | **[↑ Índice](../INTRO_INDICE.md)**
