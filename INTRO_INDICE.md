# Documentación Completa de FTC

**FIRST Tech Challenge - Guía Integral en Español**

Esta documentación cubre todos los aspectos esenciales de FTC: sistema de control, programación, sistema eléctrico, y librerías externas avanzadas como FTCLib, NextFTC, y Pedro Pathing.

---

## =Ú Tabla de Contenidos

### [1. Introducción](#1-introducción-a-ftc)
### [2. Sistema de Control](#2-sistema-de-control)
### [3. Programación](#3-programación)
### [4. Sistema Eléctrico](#4-sistema-eléctrico)
### [5. FTCLib](#5-ftclib---librería-avanzada)
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

- **[Componentes Básicos](./01_Introduccion/componentes-basicos.md)**
  - Control Hub y Expansion Hub
  - Driver Station
  - Motores DC y servos
  - Sensores (color, distancia, IMU, táctiles)
  - Cámaras y visión por computadora
  - Sistemas de construcción (REV, goBILDA, TETRIX)
  - Gamepad y controladores
  - Herramientas esenciales

- **[Configuración Inicial](./01_Introduccion/configuracion-inicial.md)**
  - Actualización de software
  - Conexión de hardware
  - Configuración del hardware en el robot
  - Instalación del SDK (Blocks, OnBot Java, Android Studio)
  - Crear y ejecutar tu primer OpMode
  - Troubleshooting común

---

## 2. Sistema de Control

### Hardware de Control

- **[Control Hub](./02_Sistema_Control/control-hub.md)**
  - Especificaciones técnicas (Snapdragon 845, puertos I/O)
  - Arquitectura del sistema
  - Configuración y uso
  - Calibración de IMU integrada
  - Actualización de firmware
  - Programación del Control Hub
  - Diagnóstico y troubleshooting
  - LEDs de estado

- **[Expansion Hub](./02_Sistema_Control/expansion-hub.md)**
  - Diferencias con Control Hub
  - Conexión mediante RS485
  - Configuración de hardware
  - Alimentación (batería separada vs compartida)
  - Consideraciones de latencia
  - Troubleshooting de comunicación

- **[Driver Station](./02_Sistema_Control/driver-station.md)**
  - Requisitos del dispositivo
  - Interfaz de usuario
  - Configuración de Wi-Fi y gamepads
  - Telemetría avanzada
  - Uso durante competencias (Autonomous y TeleOp)
  - Troubleshooting de conexión

- **[Comunicaciones](./02_Sistema_Control/comunicaciones.md)**
  - Arquitectura de comunicación (Wi-Fi Direct, RS485)
  - Configuración de Wi-Fi (bandas, canales, contraseñas)
  - Optimización de conexión
  - Verificar calidad de señal
  - Troubleshooting de lag y desconexiones
  - Seguridad y reglas de competencia
  - Herramientas avanzadas (ADB, Network Analyzer)

---

## 3. Programación

### Entornos de Desarrollo

- **[Blocks Programming](./03_Programacion/blocks-programming.md)**
  - Programación visual para principiantes
  - Categorías de bloques (Control, Lógica, Math, Hardware)
  - Crear OpModes con bloques
  - Hardware: motores, servos, sensores, gamepad
  - Ejemplos completos (Tank Drive, Autonomous, Sensores)
  - Limitaciones y cuándo cambiar a Java

- **[OnBot Java](./03_Programacion/onbot-java.md)**
  - Editor Java basado en navegador
  - Ventajas y desventajas
  - Crear OpModes en Java
  - Trabajar con hardware (motores, servos, sensores)
  - Organización de código (clases de hardware)
  - Backup y control de versiones
  - Comparación con Android Studio

- **[Android Studio](./03_Programacion/android-studio.md)**
  - Instalación y configuración
  - Estructura del proyecto FtcRobotController
  - Crear OpModes en Android Studio
  - Características avanzadas (IntelliSense, debugging, Git)
  - Instalar librerías externas
  - Mejores prácticas de desarrollo
  - Troubleshooting de compilación

### Conceptos de Programación

- **[Estructura de OpModes](./03_Programacion/estructura-opmode.md)**
  - LinearOpMode vs OpMode (Iterativo)
  - Ciclo de vida de un OpMode
  - Anotaciones (@TeleOp, @Autonomous, @Disabled)
  - Elementos clave (hardwareMap, telemetry, gamepad)
  - Patrones comunes (timeouts, state machines)
  - ¿Cuál usar?

- **[Conceptos Básicos](./03_Programacion/conceptos-basicos.md)**
  - Control PID (Proporcional-Integral-Derivativo)
  - State Machines (Máquinas de Estado)
  - Odometría (seguimiento de posición)
  - Modos de conducción (Tank, Arcade, Mecanum, Field-Centric)
  - Programación defensiva (try-catch, null checks)
  - Optimización de performance

---

## 4. Sistema Eléctrico

### Energía y Cableado

- **[Alimentación](./04_Sistema_Electrico/alimentacion.md)**
  - Tipos de baterías (NiMH, LiPo)
  - Carga y mantenimiento
  - Distribución de energía (Control Hub, Expansion Hub)
  - Gestión de corriente y límites
  - Código para ramping de potencia
  - Troubleshooting de voltaje

- **[Motores](./04_Sistema_Electrico/motores.md)**
  - Motores comunes (REV HD Hex, Core Hex, goBILDA Yellow Jacket)
  - Cálculos de encoder
  - Modos de control (RUN_WITHOUT_ENCODER, RUN_USING_ENCODER, RUN_TO_POSITION)
  - ZeroPowerBehavior (BRAKE vs FLOAT)

- **[Servos](./04_Sistema_Electrico/servos.md)**
  - Servo estándar vs continuo
  - Control de posición
  - Movimiento gradual
  - Gestión de corriente

- **[Sensores](./04_Sistema_Electrico/sensores.md)**
  - Color Sensor (REV V3)
  - Distance Sensor
  - IMU (BNO055)
  - Touch Sensor
  - Encoders externos para odometría

---

## 5. FTCLib - Librería Avanzada

### Introducción y Características

- **[Introducción a FTCLib](./05_FTCLib/introduccion-ftclib.md)**
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

- **[Introducción a NextFTC](./06_NextFTC/introduccion-nextftc.md)**
  - ¿Qué es NextFTC?
  - Instalación (incluye PedroPathing y FTC Dashboard)
  - Estructura básica (Comandos y Subsistemas)
  - Recursos y comunidad

- **[Comandos y Subsistemas](./06_NextFTC/comandos-subsistemas.md)**
  - Comandos secuenciales
  - Comandos paralelos
  - Grupos de comandos

- **[Instalación](./06_NextFTC/instalacion.md)**
  - Configuración de Gradle
  - Verificación de instalación

---

## 7. Pedro Pathing - Path Following

### Navegación Autónoma Avanzada

- **[Introducción a Pedro Pathing](./07_Pedro_Pathing/introduccion-pedro.md)**
  - ¿Qué es Pedro Pathing?
  - Características (curvas de Bézier, PIDF, corrección centrípeta)
  - Instalación
  - Configuración básica (Follower, Paths, Update Loop)
  - Path Types (Bezier Curve, Bezier Line)
  - Path Actions (Heading, Velocidad)
  - Ejemplo completo de Autonomous
  - Tuning de constantes
  - Visualizador web
  - Comparación con RoadRunner

- **[Curvas de Bézier](./07_Pedro_Pathing/bezier-curves.md)**
  - Tipos de curvas (Línea, Cuadrática, Cúbica)
  - Puntos de control

- **[Configuración](./07_Pedro_Pathing/configuracion.md)**
  - Configurar encoders de odometría
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
  - Computer Vision en FTC
  - Instalación
  - Ejemplo básico
  - EOCV-Sim (simulador)

- **[FTC Dashboard](./08_Recursos_Adicionales/ftc-dashboard.md)**
  - Telemetría avanzada en navegador
  - Instalación
  - Uso básico
  - Acceso web
  - Características (gráficos, configuración en vivo, visualización)

---

## = Enlaces Oficiales

### Recursos FIRST

- **[FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)** - Sitio oficial
- **[FTC Documentation](https://ftc-docs.firstinspires.org/)** - Documentación oficial
- **[Game Manual](https://www.firstinspires.org/resource-library/ftc/game-and-season-info)** - Reglas del juego
- **[GitHub FTC](https://github.com/FIRST-Tech-Challenge)** - SDK oficial
- **[FTC SIM](https://ftcsim.org/)** - Simulador virtual

### Comunidad y Recursos

- **[Game Manual 0 (GM0)](https://gm0.org)** - Guía de la comunidad (altamente recomendado)
- **[FTC Discord](https://discord.gg/first-tech-challenge)** - Comunidad activa
- **[Chief Delphi - FTC](https://www.chiefdelphi.com/c/technical/first-tech-challenge/)** - Foro técnico
- **[Reddit r/FTC](https://www.reddit.com/r/FTC/)** - Discusiones de equipos

### Librerías y Herramientas

- **[FTCLib Docs](https://docs.ftclib.org/)** - Documentación FTCLib
- **[Pedro Pathing](https://pedropathing.com/)** - Docs y visualizador
- **[FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/)** - Telemetría avanzada
- **[RoadRunner](https://learnroadrunner.com/)** - Path following

---

## =Ý Notas de Uso

### Navegación

- Usa los hipervínculos para moverte entre secciones
- Cada documento tiene enlaces de navegación al final:
  - ** Anterior**: Documento previo
  - **’ Siguiente**: Siguiente documento
  - **‘ Índice**: Volver a este índice

### Actualizaciones

Esta documentación se basa en la temporada **2025-2026 (DECODE)**. Verifica siempre el Game Manual oficial para:
- Reglas específicas de la temporada
- Hardware y software permitido
- Restricciones de competencia

### Contribuciones

Documentación creada como recurso educativo para equipos de FTC de habla hispana.

---

## =€ Por Dónde Empezar

### Nuevo en FTC
1. [¿Qué es FTC?](./01_Introduccion/que-es-ftc.md)
2. [Componentes Básicos](./01_Introduccion/componentes-basicos.md)
3. [Configuración Inicial](./01_Introduccion/configuracion-inicial.md)
4. [Blocks Programming](./03_Programacion/blocks-programming.md)

### Equipo con Experiencia
1. [Android Studio](./03_Programacion/android-studio.md)
2. [Conceptos Básicos de Programación](./03_Programacion/conceptos-basicos.md)
3. [FTCLib](./05_FTCLib/introduccion-ftclib.md)
4. [Pedro Pathing](./07_Pedro_Pathing/introduccion-pedro.md)

### Preparación para Competencia
1. [Sistema de Control](./02_Sistema_Control/control-hub.md)
2. [Comunicaciones](./02_Sistema_Control/comunicaciones.md)
3. [Sistema Eléctrico](./04_Sistema_Electrico/alimentacion.md)
4. [Driver Station](./02_Sistema_Control/driver-station.md)

---

**¡Éxito en tu temporada de FTC!** ><Æ

---

## Referencias

Esta documentación se compiló usando información de:
- [FIRST Tech Challenge Official Documentation](https://ftc-docs.firstinspires.org/)
- [FTCLib Documentation](https://docs.ftclib.org/)
- [Pedro Pathing Documentation](https://pedropathing.com/docs)
- [Game Manual 0](https://gm0.org)
- Experiencia de equipos de FTC
- Investigación de fuentes oficiales (2025)

**Fuentes consultadas**:
- [FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)
- [FTC Programming Resources](https://ftc-docs.firstinspires.org/en/latest/programming_resources/index.html)
- [FTCLib GitHub](https://github.com/FTCLib/FTCLib)
- [NextFTC GitHub](https://github.com/NextFTC/NextFTC)
- [Pedro Pathing Official Site](https://pedropathing.com/)

---

*Última actualización: Diciembre 2025*
