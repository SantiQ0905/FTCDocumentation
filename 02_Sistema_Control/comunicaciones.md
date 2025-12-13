# Comunicaciones en FTC - Wi-Fi y Conexiones

## Introducción

La comunicación entre el **Control Hub** y el **Driver Station** es crítica para el funcionamiento del robot. Este documento cubre Wi-Fi Direct, optimización de señal, troubleshooting de conexión, y configuraciones avanzadas para maximizar confiabilidad en competencias.

## Arquitectura de Comunicación

### Diagrama de Sistema

```
[Driver Station] <--Wi-Fi Direct--> [Control Hub] <--RS485--> [Expansion Hub]
       |                                  |
    Gamepads                         Robot Hardware
   (USB/BT)                        (Motores, Sensores)
```

### Flujo de Datos

1. **Gamepad → Driver Station**: Botones/joysticks leídos via USB/Bluetooth
2. **Driver Station → Control Hub**: Comandos enviados via Wi-Fi Direct
3. **Control Hub procesa**: OpMode ejecuta lógica
4. **Control Hub → Hardware**: Comandos a motores/servos
5. **Sensores → Control Hub**: Datos de sensores leídos
6. **Control Hub → Driver Station**: Telemetría enviada via Wi-Fi
7. **(Opcional) Control Hub → Expansion Hub**: Comandos via RS485

## Wi-Fi Direct

### ¿Qué es Wi-Fi Direct?

Wi-Fi Direct permite conexión directa entre dos dispositivos sin necesidad de router intermediario. El Control Hub actúa como **Access Point (AP)** y el Driver Station se conecta como **cliente**.

### Características

- **Protocolo**: 802.11 a/b/g/n/ac
- **Frecuencias**: 2.4 GHz y 5 GHz
- **Rango típico**: 10-30 metros (varía según interferencia)
- **Latencia típica**: 10-50 ms
- **Ancho de banda**: Suficiente para comandos y telemetría

### Configuración de Red

**Configuración por Defecto del Control Hub:**
- **SSID**: `FTC-XXXX` (XXXX = últimos 4 dígitos del S/N)
- **IP del Control Hub**: `192.168.43.1`
- **IP del Driver Station**: `192.168.43.XXX` (asignada automáticamente via DHCP)
- **Contraseña**: Ver etiqueta del Control Hub o establecida por el equipo

### Cambiar Nombre y Contraseña

#### Vía Interfaz Web

1. Conecta al Wi-Fi del Control Hub
2. Navega a: `http://192.168.43.1:8080`
3. Menú → **Manage** → **Network Settings**
4. **Access Point Name**: Cambia "FTC-XXXX" a nombre personalizado
   - Ejemplo: "Team12345-Main"
   - Sin espacios, caracteres especiales limitados
5. **Access Point Password**: Establece contraseña segura
   - Mínimo 8 caracteres
   - Combina letras, números
6. **Save** y reinicia Control Hub

#### Recomendaciones de Nombre

- **Incluye número de equipo**: "FTC12345-Robot1"
- **Descriptivo**: "RedAllianceBot" si tienes múltiples robots
- **Único**: Evita conflictos en competencias con muchos equipos
- **Sin espacios**: Usa guiones o CamelCase

### Bandas de Frecuencia

#### 2.4 GHz

**Ventajas**:
- Mayor rango
- Mejor penetración a través de obstáculos
- Compatible con todos los dispositivos

**Desventajas**:
- Más congestionada (Bluetooth, otros Wi-Fi, microondas)
- Menor ancho de banda
- Más interferencia en competencias

#### 5 GHz

**Ventajas**:
- Menos congestionada
- Mayor ancho de banda
- Menos interferencia de otros dispositivos

**Desventajas**:
- Menor rango
- No todos los dispositivos son compatibles
- Algunas competencias pueden restringir 5 GHz

**Recomendación**: Usa 5 GHz si tu Driver Station lo soporta y las reglas lo permiten. Cambia a 2.4 GHz si hay problemas de rango o compatibilidad.

#### Configurar Banda

1. Interfaz web del Control Hub: `192.168.43.1:8080`
2. **Manage** → **Network Settings**
3. **Wi-Fi Band**: Selecciona "2.4 GHz" o "5 GHz"
4. **Apply** y reconecta

### Canales Wi-Fi

#### ¿Qué son los Canales?

Los canales Wi-Fi son sub-frecuencias dentro de las bandas 2.4 GHz y 5 GHz. Seleccionar un canal no congestionado reduce interferencia.

#### Canales 2.4 GHz

- **Canales disponibles**: 1-11 (en EE.UU.)
- **Canales no superpuestos**: 1, 6, 11
- **Recomendación**: Usa canales no superpuestos para evitar interferencia

**En competencias**:
- Muchos equipos usan canal 6 (por defecto)
- Cambia a canal 1 u 11 para menos interferencia

#### Canales 5 GHz

- **Muchos más canales** disponibles (36, 40, 44, 48, etc.)
- Menos congestionados en general
- Verificar disponibilidad regional

#### Configurar Canal

**Opción 1: Automático (por defecto)**
- El Control Hub selecciona automáticamente el canal menos congestionado
- Funciona bien en la mayoría de casos

**Opción 2: Manual**
1. Interfaz web: `192.168.43.1:8080`
2. **Manage** → **Network Settings**
3. **Wi-Fi Channel**: Selecciona canal específico (1, 6, 11, etc.)
4. **Apply**

**Herramienta de análisis** (en laptop):
- **Windows**: Wi-Fi Analyzer (Microsoft Store)
- **Mac**: WiFi Explorer
- **Android**: WiFi Analyzer (Play Store)

Usa estas herramientas en el venue de la competencia para ver qué canales están menos congestionados.

## Optimización de Conexión

### Mejores Prácticas para Competencias

#### 1. Ubicación del Control Hub

- **Altura**: Montar lo más alto posible en el robot
- **Orientación**: Antena hacia arriba, sin obstrucciones metálicas
- **Protección**: Evitar envolver en metal o materiales aislantes

#### 2. Distancia

- **Mantén cercanía**: Driver Station a <10m del robot cuando sea posible
- **Línea de visión**: Minimiza obstáculos entre DS y robot
- **En pit**: Ubica el robot cerca de la mesa de trabajo

#### 3. Reducir Interferencia

**En el robot**:
- Aleja el Control Hub de motores grandes (fuentes de EMI)
- Usa cables blindados para motores si es posible
- Separa cables de potencia de cables de señal

**En el venue**:
- Apaga Wi-Fi personal cuando no esté en uso
- Desactiva hotspots móviles
- Coopera con otros equipos para distribuir canales

#### 4. Configuración del Driver Station

**En Android Settings**:
- **Wi-Fi → Advanced → Keep Wi-Fi on during sleep**: ON
- **Battery Saver**: OFF durante competencias
- **Background Apps**: Cierra apps no esenciales

**En Driver Station App**:
- **Settings → Keep Screen On**: ON
- Cierra otras apps que usan red

### Verificar Calidad de Conexión

#### Ping Test

En tu laptop conectada al Wi-Fi del Control Hub:

**Windows**:
```bash
ping 192.168.43.1 -t
```

**Mac/Linux**:
```bash
ping 192.168.43.1
```

**Interpretación**:
- **Tiempo <20ms**: Excelente
- **Tiempo 20-50ms**: Bueno
- **Tiempo >50ms**: Aceptable, puede haber lag perceptible
- **Pérdida de paquetes >5%**: Problema de conexión

#### Monitoreo en OpMode

```java
@TeleOp(name="Test de Conexión")
public class ConnectionTest extends LinearOpMode {

    private ElapsedTime loopTimer = new ElapsedTime();
    private double maxLoopTime = 0;
    private double minLoopTime = 1000;

    @Override
    public void runOpMode() {
        waitForStart();

        while (opModeIsActive()) {
            double loopTime = loopTimer.milliseconds();
            loopTimer.reset();

            maxLoopTime = Math.max(maxLoopTime, loopTime);
            minLoopTime = Math.min(minLoopTime, loopTime);

            telemetry.addData("Loop Time", "%.1f ms", loopTime);
            telemetry.addData("Max Loop Time", "%.1f ms", maxLoopTime);
            telemetry.addData("Min Loop Time", "%.1f ms", minLoopTime);

            // Advertencia si loop es muy lento
            if (loopTime > 100) {
                telemetry.addData("ADVERTENCIA", "Loop lento!");
            }

            telemetry.update();
        }
    }
}
```

**Interpretación**:
- **<20ms**: Excelente, ~50 Hz
- **20-50ms**: Bueno, ~20-50 Hz
- **>100ms**: Problema, puede causar lag notable

## Comunicación RS485 (Control Hub ↔ Expansion Hub)

### Características

- **Protocolo**: RS485 diferencial
- **Velocidad**: 115200 baud
- **Alcance**: Hasta 1200m teóricamente, 600mm cable recomendado en FTC
- **Latencia**: 1-2ms adicional vs Control Hub directo

### Cableado

**Cable RS485 Estándar**:
- 4 pines: GND, VCC, A (Data+), B (Data-)
- Conector JST PH

**Mejores Prácticas**:
1. **Ruta directa**: Evita rutas largas y enredadas
2. **Aleja de fuentes de ruido**:
   - Motores grandes
   - Cables de alta corriente
   - Fuentes de alimentación switching
3. **Fija firmemente**: Usa amarres para prevenir desconexiones
4. **Inspecciona regularmente**: Busca desgaste en el cable

### Verificar Comunicación RS485

```java
@TeleOp(name="Test RS485")
public class RS485Test extends LinearOpMode {

    @Override
    public void runOpMode() {
        // Intentar acceder a motor en Expansion Hub
        DcMotor expansionMotor = null;

        try {
            expansionMotor = hardwareMap.get(DcMotor.class, "expansionMotor");
            telemetry.addData("Expansion Hub", "CONECTADO");
        } catch (Exception e) {
            telemetry.addData("Expansion Hub", "ERROR: No detectado");
        }

        // Mostrar voltaje de ambos hubs
        for (VoltageSensor sensor : hardwareMap.voltageSensor) {
            telemetry.addData(sensor.getDeviceName(), "%.2f V", sensor.getVoltage());
        }

        telemetry.update();
        waitForStart();

        while (opModeIsActive()) {
            if (expansionMotor != null) {
                expansionMotor.setPower(gamepad1.left_stick_y);
                telemetry.addData("Motor Power", expansionMotor.getPower());
            }

            telemetry.update();
        }
    }
}
```

## Troubleshooting de Conexión

### Conexión Intermitente

**Síntomas**: Driver Station conecta/desconecta repetidamente

**Diagnóstico**:

1. **Verificar voltaje de batería**:
   - Si <11V bajo carga, cambia batería
   - Caída de voltaje puede resetear Control Hub

2. **Interferencia Wi-Fi**:
   - Cambia canal Wi-Fi
   - Usa herramienta de análisis para encontrar canal libre

3. **Sobrecarga del Control Hub**:
   - Código bloqueado en OpMode
   - Demasiados cálculos pesados
   - Reduce carga computacional

**Código de Diagnóstico**:
```java
// Agregar al loop principal
double voltage = hardwareMap.voltageSensor.iterator().next().getVoltage();
if (voltage < 11.5) {
    telemetry.addData("ADVERTENCIA", "Batería Baja: %.2f V", voltage);
}

telemetry.addData("Thread Time", "%.1f ms",
    System.currentTimeMillis() % 1000);
telemetry.update();
```

### Lag Perceptible

**Síntomas**: Retraso entre presionar botón y respuesta del robot

**Causas**:

1. **Loop bloqueado**:
```java
// MALO
while (sensor.getValue() < threshold) {
    // Espera activa, bloquea comunicación
}

// BUENO
if (sensor.getValue() < threshold) {
    // Acción no bloqueante
}
```

2. **Sleeps en TeleOp**:
```java
// EVITAR en TeleOp
sleep(100);

// USAR temporizadores
ElapsedTime timer = new ElapsedTime();
if (timer.milliseconds() > 100) {
    // Acción
    timer.reset();
}
```

3. **Telemetría excesiva**:
```java
// MALO - actualiza cada loop
telemetry.update();

// BUENO - limita frecuencia
if (loopCount % 10 == 0) {
    telemetry.update();
}
```

### Desconexión Total

**Síntomas**: No conecta en absoluto, círculo rojo permanente

**Soluciones paso a paso**:

1. **Verificar Power**:
   - Control Hub LED verde? → Sí: continúa, No: problema de batería/power
   - Driver Station cargado >50%?

2. **Verificar Wi-Fi**:
   - Driver Station conectado a red correcta?
   - Configuración Wi-Fi Android muestra "FTC-XXXX"?
   - ¿Contraseña correcta?

3. **Reinicio Secuencial**:
   ```
   1. Apaga Driver Station app
   2. Apaga Control Hub (mantén botón 3s)
   3. Espera 10 segundos
   4. Enciende Control Hub
   5. Espera LED verde (30-60s)
   6. Abre Driver Station app
   7. Debe conectar en 5-10s
   ```

4. **Factory Reset** (último recurso):
   - Interfaz web → Manage → Factory Reset
   - **ADVERTENCIA**: Borra todas las configuraciones

## Seguridad y Reglas

### Contraseñas Seguras

**Requisitos de FTC**:
- No usar contraseñas por defecto en competencias
- Mínimo 8 caracteres
- Registrar contraseña con organizadores del evento (si requerido)

**Mejores Prácticas**:
- Única para tu equipo
- Escrita en Engineering Notebook
- Conocida por todos los miembros del Drive Team
- Compartida con referees si se solicita

### Reglas de Red en Competencias

**Generalmente Prohibido**:
- Conectarse a internet durante partidos
- Acceder a recursos de red externos
- Streaming de video/audio desde el robot
- Conexiones Bluetooth entre robots (solo interno)

**Generalmente Permitido**:
- Wi-Fi Direct entre Control Hub y Driver Station
- USB entre Driver Station y gamepads/laptop (para programming)
- Comunicación RS485 entre Control Hub y Expansion Hub

**Verifica el Game Manual** de la temporada actual para reglas específicas.

### Inspección de Robot

Durante inspección, los referees pueden verificar:
- Nombre de red Wi-Fi del robot
- Contraseña registrada
- Versión de software (Control Hub y Driver Station)
- Que no haya dispositivos no autorizados conectados

## Herramientas Avanzadas

### ADB (Android Debug Bridge)

Para debugging avanzado, conecta vía USB:

```bash
# Verificar dispositivos conectados
adb devices

# Ver logs del Control Hub
adb logcat

# Acceder shell del Control Hub
adb shell

# Instalar APK
adb install FtcRobotController.apk
```

### Scrcpy (Screen Mirroring)

Para ver la pantalla del Control Hub en laptop:

```bash
# Instalar scrcpy
# Windows: choco install scrcpy
# Mac: brew install scrcpy

# Ejecutar
scrcpy
```

Útil para debugging sin pantalla táctil.

### Network Analyzer

Apps para analizar redes Wi-Fi:

**Android**:
- **WiFi Analyzer** (farproc)
- Muestra canales, fuerza de señal, interferencia

**Uso en Competencia**:
1. Instala en dispositivo Android
2. Escanea redes en el venue
3. Identifica canales menos congestionados
4. Configura Control Hub a ese canal

## Checklist de Competencia

### Antes de Llegar

- [ ] Control Hub firmware actualizado
- [ ] Driver Station app actualizada
- [ ] Contraseña Wi-Fi establecida y documentada
- [ ] Nombre de red Wi-Fi registrado
- [ ] Gamepads emparejados y probados
- [ ] Baterías cargadas (mínimo 2)

### En el Venue

- [ ] Analizar canales Wi-Fi con herramienta
- [ ] Configurar canal menos congestionado
- [ ] Verificar conexión en ubicación del campo
- [ ] Probar latencia con ping test
- [ ] Verificar que Driver Station mantiene conexión con pantalla apagada

### Antes de Cada Match

- [ ] Batería >12.5V
- [ ] Driver Station >50% carga
- [ ] Wi-Fi conectada (círculo verde)
- [ ] Gamepads detectados
- [ ] OpMode correcto seleccionado

### Después de Problemas de Conexión

- [ ] Documentar qué pasó (cuándo, dónde, síntomas)
- [ ] Revisar logs (ADB logcat si es posible)
- [ ] Verificar cables RS485
- [ ] Probar con batería diferente
- [ ] Cambiar canal Wi-Fi si fue interferencia

## Próximos Pasos

- [Programación - Estructura OpMode](../03_Programacion/estructura-opmode.md)
- [Sistema Eléctrico - Alimentación](../04_Sistema_Electrico/alimentacion.md)
- [FTC Dashboard](../08_Recursos_Adicionales/ftc-dashboard.md) - Telemetría avanzada

---

**[← Anterior: Driver Station](./driver-station.md)** | **[→ Siguiente: Programación](../03_Programacion/blocks-programming.md)** | **[↑ Índice](../INTRO_INDICE.md)**
