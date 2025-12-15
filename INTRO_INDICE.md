# Documentación Completa de FTC

**FIRST Tech Challenge - Guía Integral en Español**

Esta documentación cubre todos los aspectos esenciales de FTC: sistema de control, programación, sistema eléctrico, y librerías externas avanzadas como FTCLib, NextFTC, y Pedro Pathing.

---

## =� Tabla de Contenidos

### [1. Introducción](#1-Introducción-a-ftc)
### [2. Sistema de Control](#2-sistema-de-control)
### [3. Programación](#3-Programación)
### [4. Sistema Eléctrico](#4-sistema-Eléctrico)
### [5. FTCLib](#5-ftclib---Librería-avanzada)
### [6. NextFTC](#6-nextftc---framework-moderno)
### [7. Pedro Pathing](#7-pedro-pathing---path-following)
### [8. Recursos Adicionales](#8-recursos-adicionales)

---

## 1. Introducción a FTC

### Fundamentos

- **[¿Qué es FTC?](./01_Introduccion/que-es-ftc.md)**
  - Objetivos del programa
  - Estructura de la competencia (Autonomous + TeleOp)
  - Valores de FIRST
  - Temporada competitiva
  - Premios y oportunidades

- **[Componentes básicos](./01_Introduccion/componentes-basicos.md)**
  - Control Hub y Expansion Hub
  - Driver Station
  - Motores DC y servos
  - Sensores (color, distancia, IMU, táctiles)
  - Cámaras y visión por computadora
  - Sistemas de construcción (REV, goBILDA, TETRIX)
  - Gamepad y controladores
  - Herramientas esenciales

- **[ConfiGuíaci�n Inicial](./01_Introduccion/confiGuíacion-inicial.md)**
  - actualización de software
  - conexión de hardware
  - ConfiGuíaci�n del hardware en el robot
  - Instalación del SDK (Blocks, OnBot Java, Android Studio)
  - Crear y ejecutar tu primer OpMode
  - Troubleshooting común

---

## 2. Sistema de Control

### Hardware de Control

- **[Control Hub](./02_Sistema_Control/control-hub.md)**
  - Especificaciones técnicas (Snapdragon 845, puertos I/O)
  - A¿Quétectura del sistema
  - ConfiGuíaci�n y uso
  - Calibración de IMU integrada
  - actualización de firmware
  - Programación del Control Hub
  - Diagnóstico y troubleshooting
  - LEDs de estádo

- **[Expansion Hub](./02_Sistema_Control/expansion-hub.md)**
  - Diferencias con Control Hub
  - conexión mediante RS485
  - ConfiGuíaci�n de hardware
  - alimentación (bater�a separada vs compartida)
  - Consideraciones de latencia
  - Troubleshooting de Comunicación

- **[Driver Station](./02_Sistema_Control/driver-station.md)**
  - R¿Quésitos del dispositivo
  - Interfaz de usuario
  - ConfiGuíaci�n de Wi-Fi y gamepads
  - Telemetría avanzada
  - Uso durante competencias (Autonomous y TeleOp)
  - Troubleshooting de conexión

- **[Comunicaciónes](./02_Sistema_Control/Comunicaciónes.md)**
  - A¿Quétectura de Comunicación (Wi-Fi Direct, RS485)
  - ConfiGuíaci�n de Wi-Fi (bandas, canales, contrase�as)
  - optimización de conexión
  - Verificar calidad de señal
  - Troubleshooting de lag y desconexiónes
  - Seguridad y reglas de competencia
  - Herramientas avanzadas (ADB, Network Analyzer)

---

## 3. Programación

### Entornos de Desarrollo

- **[Blocks Programming](./03_Programación/blocks-programming.md)**
  - Programación visual para principiantes
  - Categorías de bl¿Qués (Control, Lógica, Math, Hardware)
  - Crear OpModes con bl¿Qués
  - Hardware: motores, servos, Sensores, gamepad
  - Ejemplos completos (Tank Drive, Autonomous, Sensores)
  - Limitaciones y cuándo cambiar a Java

- **[OnBot Java](./03_Programación/onbot-java.md)**
  - Editor Java basado en navegador
  - Ventajas y desventajas
  - Crear OpModes en Java
  - Trabajar con hardware (motores, servos, Sensores)
  - Organización de código (clases de hardware)
  - Backup y control de Versiónes
  - Comparación con Android Studio

- **[Android Studio](./03_Programación/android-studio.md)**
  - Instalación y confiGuíaci�n
  - Estructura del proyecto FtcRobotController
  - Crear OpModes en Android Studio
  - Características avanzadas (IntelliSense, debugging, Git)
  - Instalar librerías externas
  - Mejores pr�cticas de desarrollo
  - Troubleshooting de compilación

### Conceptos de Programación

- **[Estructura de OpModes](./03_Programación/Estructura-opmode.md)**
  - LínearOpMode vs OpMode (Iterativo)
  - Ciclo de vida de un OpMode
  - Anotaciones (@TeleOp, @Autonomous, @Disabled)
  - Elementos clave (hardwareMap, telemetry, gamepad)
  - Patrones comunes (timeouts, state machines)
  - �Cu�l usar?

- **[Conceptos básicos](./03_Programación/conceptos-básicos.md)**
  - Control PID (Proporcional-Integral-Derivativo)
  - State Machines (M¿Quénas de estádo)
  - odometría (seguimiento de posici�n)
  - Modos de conducción (Tank, Arcade, Mecanum, Field-Centric)
  - Programación defensiva (try-catch, null checks)
  - optimización de performance

---

## 4. Sistema Eléctrico

### Energía y Cableado

- **[alimentación](./04_Sistema_Eléctrico/alimentación.md)**
  - Tipos de Baterías (NiMH, LiPo)
  - Carga y mantenimiento
  - distribución de Energía (Control Hub, Expansion Hub)
  - gestáón de corriente y l�mites
  - código para ramping de potencia
  - Troubleshooting de voltaje

- **[Motores](./04_Sistema_Eléctrico/motores.md)**
  - Motores comunes (REV HD Hex, Core Hex, goBILDA Yellow Jacket)
  - cálculos de encoder
  - Modos de control (RUN_WITHOUT_ENCODER, RUN_USING_ENCODER, RUN_TO_POSITION)
  - ZeroPowerBehavior (BRAKE vs FLOAT)

- **[Servos](./04_Sistema_Eléctrico/servos.md)**
  - Servo estándar vs continuo
  - Control de posici�n
  - Movimiento gradual
  - gestáón de corriente

- **[Sensores](./04_Sistema_Eléctrico/Sensores.md)**
  - Color Sensor (REV V3)
  - Distance Sensor
  - IMU (BNO055)
  - Touch Sensor
  - Encoders externos para odometría

---

## 5. FTCLib - Librería avanzada

### Introducción y Características

- **[Introducción a FTCLib](./05_FTCLib/Introducción-ftclib.md)**
  - ¿Qué es FTCLib?
  - Instalación (Gradle)
  - Hardware Wrappers (Motor, MotorEx, SimpleServo)
  - PID Controller integrado
  - Drivetrain Classes (MecanumDrive, field-centric)
  - Command-Based Programming
  - Odometry
  - Recursos y documentación

### Componentes de FTCLib

- **[Hardware](./05_FTCLib/hardware.md)**
  - Motor Groups
  - Sensores
  - Gyro

- **[Controladores](./05_FTCLib/controladores.md)**
  - PID Controller
  - PIDF Controller (con Feedforward)

- **[Command-Based Programming](./05_FTCLib/command-base.md)**
  - Subsystems
  - Commands
  - Scheduler
  - Ejemplos completos

- **[Utilidades](./05_FTCLib/utilidades.md)**
  - Timing (Timers)
  - Range Clipping
  - Math Utils

---

## 6. NextFTC - Framework Moderno

### Framework Command-Based

- **[Introducción a NextFTC](./06_NextFTC/Introducción-nextftc.md)**
  - ¿Qué es NextFTC?
  - Instalación (incluye PedroPathing y FTC Dashboard)
  - Estructura b�sica (Comandos y Subsistemas)
  - Recursos y comunidad

- **[Comandos y Subsistemas](./06_NextFTC/comandos-subsistemas.md)**
  - Comandos secuenciales
  - Comandos paralelos
  - Grupos de comandos

- **[Instalación](./06_NextFTC/Instalación.md)**
  - ConfiGuíaci�n de Gradle
  - Verificaci�n de Instalación

---

## 7. Pedro Pathing - Path Following

### navegación autónoma avanzada

- **[Introducción a Pedro Pathing](./07_Pedro_Pathing/Introducción-pedro.md)**
  - ¿Qué es Pedro Pathing?
  - Características (curvas de Bézier, PIDF, corrección centrípeta)
  - Instalación
  - ConfiGuíaci�n b�sica (Follower, Paths, Update Loop)
  - Path Types (Bézier Curve, Bézier Line)
  - Path Actions (Heading, Velocidad)
  - Ejemplo completo de Autonomous
  - Tuning de constantes
  - Visualizador web
  - Comparación con RoadRunner

- **[Curvas de Bézier](./07_Pedro_Pathing/Bézier-curves.md)**
  - Tipos de curvas (Línea, Cuadrática, Cúbica)
  - Puntos de control

- **[ConfiGuíaci�n](./07_Pedro_Pathing/confiGuíacion.md)**
  - ConfiGuíar encoders de odometría
  - Constantes del robot
  - Tuning PID

---

## 8. Recursos Adicionales

### Herramientas y Librerías Complementarias

- **[RoadRunner](./08_Recursos_Adicionales/roadrunner.md)**
  - Path following con splines
  - Instalación
  - Recursos

- **[EasyOpenCV](./08_Recursos_Adicionales/easycv.md)**
  - Computer visión en FTC
  - Instalación
  - Ejemplo básico
  - EOCV-Sim (simulador)

- **[FTC Dashboard](./08_Recursos_Adicionales/ftc-dashboard.md)**
  - Telemetría avanzada en navegador
  - Instalación
  - Uso básico
  - Acceso web
  - Características (gráficos, confiGuíaci�n en vivo, visualizaci�n)

---

## = Enlaces Oficiales

### Recursos FIRST

- **[FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)** - Sitio oficial
- **[FTC Documentation](https://ftc-docs.firstinspires.org/)** - documentación oficial
- **[Game Manual](https://www.firstinspires.org/resource-library/ftc/game-and-season-info)** - Reglas del juego
- **[GitHub FTC](https://github.com/FIRST-Tech-Challenge)** - SDK oficial
- **[FTC SIM](https://ftcsim.org/)** - Simulador virtual

### Comunidad y Recursos

- **[Game Manual 0 (GM0)](https://gm0.org)** - Guía de la comunidad (altamente recomendado)
- **[FTC Discord](https://discord.gg/first-tech-challenge)** - Comunidad activa
- **[Chief Delphi - FTC](https://www.chiefdelphi.com/c/technical/first-tech-challenge/)** - Foro técnico
- **[Reddit r/FTC](https://www.reddit.com/r/FTC/)** - Discusiones de ¿Quépos

### Librerías y Herramientas

- **[FTCLib Docs](https://docs.ftclib.org/)** - documentación FTCLib
- **[Pedro Pathing](https://pedropathing.com/)** - Docs y Visualizador
- **[FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/)** - Telemetría avanzada
- **[RoadRunner](https://learnroadrunner.com/)** - Path following

---

## =� Notas de Uso

### navegación

- Usa los hiperv�nculos para moverte entre secciones
- Cada documento tiene enlaces de navegación al final:
  - **� Anterior**: Documento previo
  - **� Siguiente**: Siguiente documento
  - **� Índice**: Volver a está Índice

### actualizaciónes

Esta documentación se basa en la Temporada **2025-2026 (DECODE)**. Verifica siempre el Game Manual oficial para:
- Reglas específicas de la Temporada
- Hardware y software permitido
- Restáicciones de competencia

### Contribuciones

documentación creada Cómo recurso educativo para ¿Quépos de FTC de habla hispana.

---

## =� Por dónde Empezar

### Nuevo en FTC
1. [¿Qué es FTC?](./01_Introduccion/que-es-ftc.md)
2. [Componentes básicos](./01_Introduccion/componentes-basicos.md)
3. [ConfiGuíaci�n Inicial](./01_Introduccion/confiGuíacion-inicial.md)
4. [Blocks Programming](./03_Programación/blocks-programming.md)

### ¿Quépo con Experiencia
1. [Android Studio](./03_Programación/android-studio.md)
2. [Conceptos básicos de Programación](./03_Programación/conceptos-básicos.md)
3. [FTCLib](./05_FTCLib/Introducción-ftclib.md)
4. [Pedro Pathing](./07_Pedro_Pathing/Introducción-pedro.md)

### Preparaci�n para Competencia
1. [Sistema de Control](./02_Sistema_Control/control-hub.md)
2. [Comunicaciónes](./02_Sistema_Control/Comunicaciónes.md)
3. [Sistema Eléctrico](./04_Sistema_Eléctrico/alimentación.md)
4. [Driver Station](./02_Sistema_Control/driver-station.md)

---

**�Éxito en tu Temporada de FTC!** ><�

---

## Referencias

Esta documentación se compil� usando informaci�n de:
- [FIRST Tech Challenge Official Documentation](https://ftc-docs.firstinspires.org/)
- [FTCLib Documentation](https://docs.ftclib.org/)
- [Pedro Pathing Documentation](https://pedropathing.com/docs)
- [Game Manual 0](https://gm0.org)
- Experiencia de ¿Quépos de FTC
- Investágaci�n de fuentes oficiales (2025)

**Fuentes consultadas**:
- [FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)
- [FTC Programming Resources](https://ftc-docs.firstinspires.org/en/latestáprogramming_resources/index.html)
- [FTCLib GitHub](https://github.com/FTCLib/FTCLib)
- [NextFTC GitHub](https://github.com/NextFTC/NextFTC)
- [Pedro Pathing Official Site](https://pedropathing.com/)

---

*Última actualización: Diciembre 2025*
