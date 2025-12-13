# Documentaci�n Completa de FTC

**FIRST Tech Challenge - Gu�a Integral en Espa�ol**

Esta documentaci�n cubre todos los aspectos esenciales de FTC: sistema de control, programaci�n, sistema el�ctrico, y librer�as externas avanzadas como FTCLib, NextFTC, y Pedro Pathing.

---

## =� Tabla de Contenidos

### [1. Introducci�n](#1-introducci�n-a-ftc)
### [2. Sistema de Control](#2-sistema-de-control)
### [3. Programaci�n](#3-programaci�n)
### [4. Sistema El�ctrico](#4-sistema-el�ctrico)
### [5. FTCLib](#5-ftclib---librer�a-avanzada)
### [6. NextFTC](#6-nextftc---framework-moderno)
### [7. Pedro Pathing](#7-pedro-pathing---path-following)
### [8. Recursos Adicionales](#8-recursos-adicionales)

---

## 1. Introducci�n a FTC

### Fundamentos

- **[�Qu� es FTC?](./01_Introduccion/que-es-ftc.md)**
  - Objetivos del programa
  - Estructura de la competencia (Autonomous + TeleOp)
  - Valores de FIRST
  - Temporada competitiva
  - Premios y oportunidades

- **[Componentes B�sicos](./01_Introduccion/componentes-basicos.md)**
  - Control Hub y Expansion Hub
  - Driver Station
  - Motores DC y servos
  - Sensores (color, distancia, IMU, t�ctiles)
  - C�maras y visi�n por computadora
  - Sistemas de construcci�n (REV, goBILDA, TETRIX)
  - Gamepad y controladores
  - Herramientas esenciales

- **[Configuraci�n Inicial](./01_Introduccion/configuracion-inicial.md)**
  - Actualizaci�n de software
  - Conexi�n de hardware
  - Configuraci�n del hardware en el robot
  - Instalaci�n del SDK (Blocks, OnBot Java, Android Studio)
  - Crear y ejecutar tu primer OpMode
  - Troubleshooting com�n

---

## 2. Sistema de Control

### Hardware de Control

- **[Control Hub](./02_Sistema_Control/control-hub.md)**
  - Especificaciones t�cnicas (Snapdragon 845, puertos I/O)
  - Arquitectura del sistema
  - Configuraci�n y uso
  - Calibraci�n de IMU integrada
  - Actualizaci�n de firmware
  - Programaci�n del Control Hub
  - Diagn�stico y troubleshooting
  - LEDs de estado

- **[Expansion Hub](./02_Sistema_Control/expansion-hub.md)**
  - Diferencias con Control Hub
  - Conexi�n mediante RS485
  - Configuraci�n de hardware
  - Alimentaci�n (bater�a separada vs compartida)
  - Consideraciones de latencia
  - Troubleshooting de comunicaci�n

- **[Driver Station](./02_Sistema_Control/driver-station.md)**
  - Requisitos del dispositivo
  - Interfaz de usuario
  - Configuraci�n de Wi-Fi y gamepads
  - Telemetr�a avanzada
  - Uso durante competencias (Autonomous y TeleOp)
  - Troubleshooting de conexi�n

- **[Comunicaciones](./02_Sistema_Control/comunicaciones.md)**
  - Arquitectura de comunicaci�n (Wi-Fi Direct, RS485)
  - Configuraci�n de Wi-Fi (bandas, canales, contrase�as)
  - Optimizaci�n de conexi�n
  - Verificar calidad de se�al
  - Troubleshooting de lag y desconexiones
  - Seguridad y reglas de competencia
  - Herramientas avanzadas (ADB, Network Analyzer)

---

## 3. Programaci�n

### Entornos de Desarrollo

- **[Blocks Programming](./03_Programacion/blocks-programming.md)**
  - Programaci�n visual para principiantes
  - Categor�as de bloques (Control, L�gica, Math, Hardware)
  - Crear OpModes con bloques
  - Hardware: motores, servos, sensores, gamepad
  - Ejemplos completos (Tank Drive, Autonomous, Sensores)
  - Limitaciones y cu�ndo cambiar a Java

- **[OnBot Java](./03_Programacion/onbot-java.md)**
  - Editor Java basado en navegador
  - Ventajas y desventajas
  - Crear OpModes en Java
  - Trabajar con hardware (motores, servos, sensores)
  - Organizaci�n de c�digo (clases de hardware)
  - Backup y control de versiones
  - Comparaci�n con Android Studio

- **[Android Studio](./03_Programacion/android-studio.md)**
  - Instalaci�n y configuraci�n
  - Estructura del proyecto FtcRobotController
  - Crear OpModes en Android Studio
  - Caracter�sticas avanzadas (IntelliSense, debugging, Git)
  - Instalar librer�as externas
  - Mejores pr�cticas de desarrollo
  - Troubleshooting de compilaci�n

### Conceptos de Programaci�n

- **[Estructura de OpModes](./03_Programacion/estructura-opmode.md)**
  - LinearOpMode vs OpMode (Iterativo)
  - Ciclo de vida de un OpMode
  - Anotaciones (@TeleOp, @Autonomous, @Disabled)
  - Elementos clave (hardwareMap, telemetry, gamepad)
  - Patrones comunes (timeouts, state machines)
  - �Cu�l usar?

- **[Conceptos B�sicos](./03_Programacion/conceptos-basicos.md)**
  - Control PID (Proporcional-Integral-Derivativo)
  - State Machines (M�quinas de Estado)
  - Odometr�a (seguimiento de posici�n)
  - Modos de conducci�n (Tank, Arcade, Mecanum, Field-Centric)
  - Programaci�n defensiva (try-catch, null checks)
  - Optimizaci�n de performance

---

## 4. Sistema El�ctrico

### Energ�a y Cableado

- **[Alimentaci�n](./04_Sistema_Electrico/alimentacion.md)**
  - Tipos de bater�as (NiMH, LiPo)
  - Carga y mantenimiento
  - Distribuci�n de energ�a (Control Hub, Expansion Hub)
  - Gesti�n de corriente y l�mites
  - C�digo para ramping de potencia
  - Troubleshooting de voltaje

- **[Motores](./04_Sistema_Electrico/motores.md)**
  - Motores comunes (REV HD Hex, Core Hex, goBILDA Yellow Jacket)
  - C�lculos de encoder
  - Modos de control (RUN_WITHOUT_ENCODER, RUN_USING_ENCODER, RUN_TO_POSITION)
  - ZeroPowerBehavior (BRAKE vs FLOAT)

- **[Servos](./04_Sistema_Electrico/servos.md)**
  - Servo est�ndar vs continuo
  - Control de posici�n
  - Movimiento gradual
  - Gesti�n de corriente

- **[Sensores](./04_Sistema_Electrico/sensores.md)**
  - Color Sensor (REV V3)
  - Distance Sensor
  - IMU (BNO055)
  - Touch Sensor
  - Encoders externos para odometr�a

---

## 5. FTCLib - Librer�a Avanzada

### Introducci�n y Caracter�sticas

- **[Introducci�n a FTCLib](./05_FTCLib/introduccion-ftclib.md)**
  - �Qu� es FTCLib?
  - Instalaci�n (Gradle)
  - Hardware Wrappers (Motor, MotorEx, SimpleServo)
  - PID Controller integrado
  - Drivetrain Classes (MecanumDrive, field-centric)
  - Command-Based Programming
  - Odometry
  - Recursos y documentaci�n

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

- **[Introducci�n a NextFTC](./06_NextFTC/introduccion-nextftc.md)**
  - �Qu� es NextFTC?
  - Instalaci�n (incluye PedroPathing y FTC Dashboard)
  - Estructura b�sica (Comandos y Subsistemas)
  - Recursos y comunidad

- **[Comandos y Subsistemas](./06_NextFTC/comandos-subsistemas.md)**
  - Comandos secuenciales
  - Comandos paralelos
  - Grupos de comandos

- **[Instalaci�n](./06_NextFTC/instalacion.md)**
  - Configuraci�n de Gradle
  - Verificaci�n de instalaci�n

---

## 7. Pedro Pathing - Path Following

### Navegaci�n Aut�noma Avanzada

- **[Introducci�n a Pedro Pathing](./07_Pedro_Pathing/introduccion-pedro.md)**
  - �Qu� es Pedro Pathing?
  - Caracter�sticas (curvas de B�zier, PIDF, correcci�n centr�peta)
  - Instalaci�n
  - Configuraci�n b�sica (Follower, Paths, Update Loop)
  - Path Types (Bezier Curve, Bezier Line)
  - Path Actions (Heading, Velocidad)
  - Ejemplo completo de Autonomous
  - Tuning de constantes
  - Visualizador web
  - Comparaci�n con RoadRunner

- **[Curvas de B�zier](./07_Pedro_Pathing/bezier-curves.md)**
  - Tipos de curvas (L�nea, Cuadr�tica, C�bica)
  - Puntos de control

- **[Configuraci�n](./07_Pedro_Pathing/configuracion.md)**
  - Configurar encoders de odometr�a
  - Constantes del robot
  - Tuning PID

---

## 8. Recursos Adicionales

### Herramientas y Librer�as Complementarias

- **[RoadRunner](./08_Recursos_Adicionales/roadrunner.md)**
  - Path following con splines
  - Instalaci�n
  - Recursos

- **[EasyOpenCV](./08_Recursos_Adicionales/easycv.md)**
  - Computer Vision en FTC
  - Instalaci�n
  - Ejemplo b�sico
  - EOCV-Sim (simulador)

- **[FTC Dashboard](./08_Recursos_Adicionales/ftc-dashboard.md)**
  - Telemetr�a avanzada en navegador
  - Instalaci�n
  - Uso b�sico
  - Acceso web
  - Caracter�sticas (gr�ficos, configuraci�n en vivo, visualizaci�n)

---

## = Enlaces Oficiales

### Recursos FIRST

- **[FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)** - Sitio oficial
- **[FTC Documentation](https://ftc-docs.firstinspires.org/)** - Documentaci�n oficial
- **[Game Manual](https://www.firstinspires.org/resource-library/ftc/game-and-season-info)** - Reglas del juego
- **[GitHub FTC](https://github.com/FIRST-Tech-Challenge)** - SDK oficial
- **[FTC SIM](https://ftcsim.org/)** - Simulador virtual

### Comunidad y Recursos

- **[Game Manual 0 (GM0)](https://gm0.org)** - Gu�a de la comunidad (altamente recomendado)
- **[FTC Discord](https://discord.gg/first-tech-challenge)** - Comunidad activa
- **[Chief Delphi - FTC](https://www.chiefdelphi.com/c/technical/first-tech-challenge/)** - Foro t�cnico
- **[Reddit r/FTC](https://www.reddit.com/r/FTC/)** - Discusiones de equipos

### Librer�as y Herramientas

- **[FTCLib Docs](https://docs.ftclib.org/)** - Documentaci�n FTCLib
- **[Pedro Pathing](https://pedropathing.com/)** - Docs y visualizador
- **[FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/)** - Telemetr�a avanzada
- **[RoadRunner](https://learnroadrunner.com/)** - Path following

---

## =� Notas de Uso

### Navegaci�n

- Usa los hiperv�nculos para moverte entre secciones
- Cada documento tiene enlaces de navegaci�n al final:
  - **� Anterior**: Documento previo
  - **� Siguiente**: Siguiente documento
  - **� �ndice**: Volver a este �ndice

### Actualizaciones

Esta documentaci�n se basa en la temporada **2025-2026 (DECODE)**. Verifica siempre el Game Manual oficial para:
- Reglas espec�ficas de la temporada
- Hardware y software permitido
- Restricciones de competencia

### Contribuciones

Documentaci�n creada como recurso educativo para equipos de FTC de habla hispana.

---

## =� Por D�nde Empezar

### Nuevo en FTC
1. [�Qu� es FTC?](./01_Introduccion/que-es-ftc.md)
2. [Componentes B�sicos](./01_Introduccion/componentes-basicos.md)
3. [Configuraci�n Inicial](./01_Introduccion/configuracion-inicial.md)
4. [Blocks Programming](./03_Programacion/blocks-programming.md)

### Equipo con Experiencia
1. [Android Studio](./03_Programacion/android-studio.md)
2. [Conceptos B�sicos de Programaci�n](./03_Programacion/conceptos-basicos.md)
3. [FTCLib](./05_FTCLib/introduccion-ftclib.md)
4. [Pedro Pathing](./07_Pedro_Pathing/introduccion-pedro.md)

### Preparaci�n para Competencia
1. [Sistema de Control](./02_Sistema_Control/control-hub.md)
2. [Comunicaciones](./02_Sistema_Control/comunicaciones.md)
3. [Sistema El�ctrico](./04_Sistema_Electrico/alimentacion.md)
4. [Driver Station](./02_Sistema_Control/driver-station.md)

---

**��xito en tu temporada de FTC!** ><�

---

## Referencias

Esta documentaci�n se compil� usando informaci�n de:
- [FIRST Tech Challenge Official Documentation](https://ftc-docs.firstinspires.org/)
- [FTCLib Documentation](https://docs.ftclib.org/)
- [Pedro Pathing Documentation](https://pedropathing.com/docs)
- [Game Manual 0](https://gm0.org)
- Experiencia de equipos de FTC
- Investigaci�n de fuentes oficiales (2025)

**Fuentes consultadas**:
- [FIRST Tech Challenge Official](https://www.firstinspires.org/programs/ftc/)
- [FTC Programming Resources](https://ftc-docs.firstinspires.org/en/latest/programming_resources/index.html)
- [FTCLib GitHub](https://github.com/FTCLib/FTCLib)
- [NextFTC GitHub](https://github.com/NextFTC/NextFTC)
- [Pedro Pathing Official Site](https://pedropathing.com/)

---

*�ltima actualizaci�n: Diciembre 2025*
