# Android Studio - Entorno de Desarrollo Profesional para FTC

## Introducción

**Android Studio** es el IDE oficial para desarrollo de aplicaciones Android y el entorno más avanzado para programación FTC. Ofrece herramientas profesionales de desarrollo, debugging, y control de versiones.

## Instalación y Configuración

### Requisitos del Sistema

**Mínimo**:
- OS: Windows 10, macOS 10.14+, o Linux compatible
- RAM: 8 GB
- Almacenamiento: 10 GB libres
- Procesador: Intel i5 o equivalente

**Recomendado**:
- RAM: 16 GB
- SSD con 20+ GB libres
- Procesador: Intel i7 o equivalente

### Descargar e Instalar

#### 1. Descargar Android Studio

1. Visita: https://developer.android.com/studio
2. Descarga la versión más reciente
3. Ejecuta el instalador

#### 2. Configuración Inicial

1. Sigue el wizard de instalación
2. Selecciona "Standard" install
3. Acepta licencias de Android SDK
4. Espera a que descargue componentes (15-30 minutos)

### Clonar FtcRobotController

#### Opción A: Git Command Line

```bash
git clone https://github.com/FIRST-Tech-Challenge/FtcRobotController.git
cd FtcRobotController
```

#### Opción B: GitHub Desktop

1. Descarga GitHub Desktop: https://desktop.github.com/
2. File → Clone Repository
3. URL: `https://github.com/FIRST-Tech-Challenge/FtcRobotController.git`
4. Elige ubicación local

#### Opción C: Descarga ZIP

1. Visita: https://github.com/FIRST-Tech-Challenge/FtcRobotController
2. Code → Download ZIP
3. Extrae a carpeta local

### Abrir Proyecto en Android Studio

1. Abre Android Studio
2. File → Open
3. Navega a carpeta `FtcRobotController`
4. Selecciona la carpeta raíz
5. Clic "OK"
6. Espera a Gradle Sync (5-15 minutos primera vez)

### Configurar SDK

1. Tools → SDK Manager
2. SDK Platforms:
   - ✓ Android 8.0 (Oreo) - API 26
   - ✓ Android 8.1 (Oreo) - API 27
3. SDK Tools:
   - ✓ Android SDK Build-Tools
   - ✓ Android SDK Platform-Tools
   - ✓ Android SDK Tools
4. Apply → OK

## Estructura del Proyecto

```
FtcRobotController/
├── FtcRobotController/     # Módulo del Robot Controller
│   └── src/main/java/
├── TeamCode/               # TU CÓDIGO VA AQUÍ
│   └── src/main/java/org/firstinspires/ftc/teamcode/
│       ├── MiOpMode.java
│       ├── RobotHardware.java
│       └── (tus otros archivos)
├── build.gradle            # Configuración de Gradle
├── gradle.properties
└── README.md
```

**Importante**: TODO tu código va en la carpeta `TeamCode/src/main/java/org/firstinspires/ftc/teamcode/`

## Crear tu Primer OpMode

### 1. Crear Archivo Java

1. En Android Studio, navega a:
   - TeamCode → src → main → java → org.firstinspires.ftc.teamcode
2. Click derecho → New → Java Class
3. Nombre: `MiPrimerOpMode`
4. Kind: Class

### 2. Escribir Código

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;

@TeleOp(name="Mi Primer OpMode", group="Linear Opmode")
public class MiPrimerOpMode extends LinearOpMode {

    private DcMotor leftMotor;
    private DcMotor rightMotor;

    @Override
    public void runOpMode() {
        // Inicializar hardware
        leftMotor = hardwareMap.get(DcMotor.class, "leftMotor");
        rightMotor = hardwareMap.get(DcMotor.class, "rightMotor");

        leftMotor.setDirection(DcMotor.Direction.FORWARD);
        rightMotor.setDirection(DcMotor.Direction.REVERSE);

        telemetry.addData("Status", "Initialized");
        telemetry.update();

        waitForStart();

        while (opModeIsActive()) {
            double leftPower = -gamepad1.left_stick_y;
            double rightPower = -gamepad1.right_stick_y;

            leftMotor.setPower(leftPower);
            rightMotor.setPower(rightPower);

            telemetry.addData("Left", leftPower);
            telemetry.addData("Right", rightPower);
            telemetry.update();
        }
    }
}
```

### 3. Compilar y Desplegar

#### Conectar Dispositivo

**Opción A: Control Hub via USB**
1. Conecta Control Hub a laptop con cable USB
2. Verifica que Android Studio detecte el dispositivo
3. En barra superior: Dispositivo debe aparecer

**Opción B: Driver Station (Wireless Deployment)**
1. Conecta Driver Station via USB
2. Habilita USB Debugging en Driver Station
3. Autoriza la conexión

#### Compilar e Instalar

1. En barra superior, selecciona:
   - Module: **TeamCode**
   - Device: **Control Hub** o **Driver Station**
2. Clic botón **Run** (▶ verde)
3. Espera compilación e instalación (1-5 minutos)
4. App se instalará en el dispositivo automáticamente

## Características Avanzadas de Android Studio

### IntelliSense y Autocompletado

- **Ctrl + Space**: Autocompletado
- **Ctrl + P**: Mostrar parámetros de función
- **Ctrl + Q**: Quick documentation
- **Alt + Enter**: Quick fix (sugerencias de corrección)

### Navegación de Código

- **Ctrl + Click**: Ir a definición
- **Ctrl + B**: Ir a declaración
- **Alt + ← / →**: Navegar atrás/adelante
- **Ctrl + F12**: Ver estructura de clase
- **Ctrl + H**: Ver jerarquía de clases

### Refactoring

- **Shift + F6**: Renombrar (variable, clase, método)
- **Ctrl + Alt + M**: Extraer método
- **Ctrl + Alt + V**: Extraer variable
- **Ctrl + Alt + C**: Extraer constante

### Debugging

#### Establecer Breakpoints

1. Clic en margen izquierdo junto al número de línea
2. Aparece punto rojo (breakpoint)
3. El programa se detendrá en esa línea

#### Iniciar Debug

1. Selecciona dispositivo
2. Clic **Debug** (🐞 icono)
3. Cuando alcance breakpoint, programa se pausa

#### Controles de Debug

- **Step Over (F8)**: Ejecuta línea actual, no entra en funciones
- **Step Into (F7)**: Entra en función
- **Step Out (Shift + F8)**: Sale de función actual
- **Resume (F9)**: Continúa ejecución

#### Inspeccionar Variables

- En modo debug, panel "Variables" muestra valores
- Hover sobre variable en código para ver valor
- Click derecho → **Add to Watches** para monitoreo continuo

### Control de Versiones (Git)

#### Inicializar Git

1. VCS → Enable Version Control Integration
2. Selecciona "Git"
3. Repositorio Git se crea en la carpeta del proyecto

#### Commit Cambios

1. VCS → Commit (Ctrl + K)
2. Selecciona archivos a commitear
3. Escribe mensaje descriptivo
4. Clic **Commit**

#### Ver Historial

- VCS → Git → Show History
- Ver todos los commits previos
- Comparar versiones

#### Branches

- Git → Branches
- New Branch: Para nuevas características
- Checkout: Cambiar de branch

## Instalar Librerías Externas

### FTCLib

Archivo: `TeamCode/build.gradle`

```gradle
dependencies {
    implementation 'org.ftclib.ftclib:core:2.1.1'
}
```

### RoadRunner

```gradle
repositories {
    maven { url = 'https://maven.brott.dev/' }
}

dependencies {
    implementation 'com.acmerobotics.roadrunner:core:0.5.6'
}
```

### Pedro Pathing

```gradle
dependencies {
    implementation 'com.github.Pedro-Pathing:PedroPathing:v1.0.0'
}
```

### FTC Dashboard

```gradle
dependencies {
    implementation 'com.acmerobotics.dashboard:dashboard:0.4.12'
}
```

Después de agregar dependencias:
1. Clic **Sync Now** (banner superior)
2. Espera a que Gradle sincronice

## Mejores Prácticas

### Organización de Código

```
teamcode/
├── autonomous/
│   ├── AutonomoRojo.java
│   └── AutonomoAzul.java
├── teleop/
│   ├── TeleOpPrincipal.java
│   └── TeleOpPrueba.java
├── subsystems/
│   ├── Drivetrain.java
│   ├── Intake.java
│   └── Lift.java
├── util/
│   ├── Constants.java
│   └── Util.java
└── RobotHardware.java
```

### Constantes en Archivo Separado

`Constants.java`:
```java
package org.firstinspires.ftc.teamcode.util;

public class Constants {
    // Drivetrain
    public static final double DRIVE_SPEED = 0.8;
    public static final double TURN_SPEED = 0.5;

    // Encoders
    public static final double COUNTS_PER_MOTOR_REV = 537.7;
    public static final double WHEEL_DIAMETER_INCHES = 4.0;
    public static final double COUNTS_PER_INCH =
        COUNTS_PER_MOTOR_REV / (WHEEL_DIAMETER_INCHES * Math.PI);

    // Servo positions
    public static final double CLAW_OPEN = 0.5;
    public static final double CLAW_CLOSED = 0.0;
}
```

### Logging y Telemetría

```java
import com.qualcomm.robotcore.util.RobotLog;

// En código
RobotLog.dd("TAG", "Mensaje de debug");
RobotLog.ii("TAG", "Información");
RobotLog.ww("TAG", "Advertencia");
RobotLog.ee("TAG", "Error");

// Ver logs con ADB
adb logcat -s TAG
```

## Troubleshooting

### Gradle Sync Failed

**Solución**:
1. File → Invalidate Caches → Invalidate and Restart
2. Verifica conexión a internet
3. Borra carpeta `.gradle` y sincroniza de nuevo

### Device Not Detected

**Solución**:
1. Verifica cable USB funcional
2. Habilita USB Debugging en dispositivo Android
3. Instala drivers ADB si es Windows
4. Prueba con otro puerto USB

### Build Failed

**Solución**:
1. Lee mensaje de error en "Build" tab
2. Verifica sintaxis Java
3. Asegura que todas las importaciones son correctas
4. Build → Clean Project → Rebuild Project

### App Crashes al Iniciar

**Solución**:
1. Revisa Logcat para stack trace
2. Verifica nombres de hardware coinciden con configuración
3. Verifica que llamadas a hardware estén en try-catch

## Comparación: Android Studio vs OnBot Java

| Característica | Android Studio | OnBot Java |
|----------------|----------------|------------|
| Potencia | ★★★★★ | ★★★☆☆ |
| Facilidad | ★★☆☆☆ | ★★★★★ |
| Debugging | ★★★★★ | ★★☆☆☆ |
| Git Integration | ★★★★★ | ★☆☆☆☆ |
| Librerías Externas | ★★★★★ | ★★★☆☆ |
| Velocidad Compilación | ★★★☆☆ | ★★★★★ |

## Próximos Pasos

- [Estructura OpMode](./estructura-opmode.md) - Entender OpModes en profundidad
- [Conceptos Básicos](./conceptos-basicos.md) - Algoritmos y patrones
- [FTCLib](../05_FTCLib/introduccion-ftclib.md) - Usar librerías avanzadas

---

**[← Anterior: OnBot Java](./onbot-java.md)** | **[→ Siguiente: Estructura OpMode](./estructura-opmode.md)** | **[↑ Índice](../INTRO_INDICE.md)**
