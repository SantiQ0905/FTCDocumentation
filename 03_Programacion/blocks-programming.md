# Programación con Blocks - FTC para Principiantes

## Introducción

**FTC Blocks** es un entorno de programación visual basado en Google Blockly, diseñado específicamente para equipos que están comenzando en FTC. Permite crear programas completos arrastrando y soltando bloques, sin necesidad de escribir código.

## Acceso a Blocks

### Requisitos

- Control Hub configurado y encendido
- Driver Station o laptop conectada al Wi-Fi del Control Hub
- Navegador web moderno (Chrome, Firefox, Edge)

### Abrir el Editor

1. Conecta al Wi-Fi del Control Hub: `FTC-XXXX`
2. Abre navegador web
3. Navega a: `http://192.168.43.1:8080`
4. Clic en **"Blocks"**
5. El editor de Blocks se abrirá en tu navegador

### Interfaz del Editor

```
┌────────────────────────────────────────────────────────────────┐
│ [Nuevo] [Abrir] [Guardar] [►Compilar] [?Ayuda]               │
├─────────────────┬──────────────────────────────────────────────┤
│                 │                                              │
│  Bloques:       │         Área de Trabajo                      │
│  ◉ Control      │                                              │
│  ◉ Lógica       │     [Arrastrar bloques aquí]               │
│  ◉ Math         │                                              │
│  ◉ Variables    │                                              │
│  ◉ Funciones    │                                              │
│  ◉ DcMotor      │                                              │
│  ◉ Servo        │                                              │
│  ◉ Sensores     │                                              │
│  ◉ Gamepad      │                                              │
│  ◉ Telemetry    │                                              │
│                 │                                              │
└─────────────────┴──────────────────────────────────────────────┘
```

## Crear tu Primer OpMode

### Paso 1: Nuevo OpMode

1. Clic en **"+"** (Nuevo)
2. Selecciona tipo:
   - **LinearOpMode**: Más común, estructura secuencial
   - **OpMode**: Avanzado, basado en métodos loop()
3. Nombre: `MiPrimerOpMode`
4. Tipo de OpMode:
   - **TeleOp**: Para control manual
   - **Autonomous**: Para período autónomo

### Paso 2: Estructura Básica

Todo OpMode en Blocks tiene esta estructura:

```
┌────────────────────────────────────────┐
│  ◐ Ejecutar OpMode                    │
│  ├─ Poner TeleOp                       │
│  ├─ Poner comentario "Mi primer robot" │
│  │                                      │
│  ├─ Llamar Initialize                  │
│  │  └─ [Inicialización de hardware]   │
│  │                                      │
│  ├─ Esperar Start                      │
│  │                                      │
│  └─ Mientras OpModeIsActive            │
│     └─ [Loop principal]                │
└────────────────────────────────────────┘
```

### Paso 3: Inicializar Hardware

En la sección **"Llamar Initialize"**:

1. Arrastra bloque **"Declarar DcMotor"** desde categoría **DcMotor**
2. Configura:
   - Nombre de variable: `motorIzquierdo`
   - Nombre en configuración: `"leftMotor"` (entre comillas)
3. Repite para otros motores:
   - `motorDerecho` → `"rightMotor"`

**Ejemplo visual**:
```
Declarar motorIzquierdo como DcMotor "leftMotor"
Declarar motorDerecho como DcMotor "rightMotor"
Poner dirección motorIzquierdo a FORWARD
Poner dirección motorDerecho a REVERSE
```

### Paso 4: Loop Principal

Dentro del bloque **"Mientras OpModeIsActive"**:

```
┌─────────────────────────────────────────────┐
│ Mientras OpModeIsActive                     │
│ ├─ Poner variable potenciaIzq a             │
│ │  └─ Negar (joystick Y gamepad1 izquierdo)│
│ │                                            │
│ ├─ Poner variable potenciaDer a             │
│ │  └─ Negar (joystick Y gamepad1 derecho)  │
│ │                                            │
│ ├─ Poner potencia motorIzquierdo a potenciaIzq │
│ ├─ Poner potencia motorDerecho a potenciaDer │
│ │                                            │
│ └─ Telemetry addData "Izq" potenciaIzq     │
│    Telemetry addData "Der" potenciaDer     │
│    Telemetry update                         │
└─────────────────────────────────────────────┘
```

### Paso 5: Guardar y Compilar

1. **Guardar**: Clic en icono de guardar (💾)
   - Los OpModes se guardan automáticamente en el Control Hub
2. **Compilar**: Clic en **"►Build Everything"**
   - Espera a que compile (ver consola inferior)
   - Si hay errores, aparecerán en rojo
3. **Ejecutar**: Desde Driver Station, selecciona tu OpMode

## Categorías de Bloques

### 1. Control

Bloques para control de flujo del programa:

#### OpMode
- **Ejecutar OpMode**: Bloque raíz, todo va dentro
- **Esperar Start**: Espera a que se presione INIT → START
- **Mientras OpModeIsActive**: Loop principal del programa
- **OpModeIsActive**: Verifica si el OpMode sigue activo (booleano)

#### Condicionales
- **Si... entonces...**: Ejecuta código si condición es verdadera
- **Si... entonces... sino...**: Ejecuta código A o código B
- **Si... entonces... sino si...**: Múltiples condiciones

```
Si (botón A gamepad1 está presionado)
  entonces
    Poner potencia motor a 0.5
  sino
    Poner potencia motor a 0
```

#### Bucles
- **Repetir N veces**: Ejecuta código N veces
- **Mientras**: Ejecuta mientras condición sea verdadera
- **Para cada**: Itera sobre rango de números

### 2. Lógica

Operaciones lógicas y comparaciones:

- **Verdadero/Falso**: Valores booleanos
- **Y/O/No**: Operadores lógicos
- **= ≠ < > ≤ ≥**: Comparadores

```
Si ((potencia > 0.5) Y (sensor toca))
  entonces
    Detener motor
```

### 3. Math

Operaciones matemáticas:

- **+, -, ×, ÷**: Operaciones básicas
- **Potencia, Raíz, Absoluto**: Funciones matemáticas
- **Redondear, Piso, Techo**: Redondeo
- **Seno, Coseno, Tangente**: Trigonometría
- **Número aleatorio**: Genera número al azar

```
Poner potencia a (joystick Y) × (0.5)  // Reducir velocidad 50%
```

### 4. Variables

Crear y usar variables:

- **Declarar variable**: Crea nueva variable
- **Poner variable a**: Asigna valor
- **Cambiar variable por**: Incrementa/decrementa

```
Declarar variable velocidadMaxima = 1.0
Poner potencia motor a velocidadMaxima
```

### 5. Funciones

Crear funciones reutilizables:

```
┌─────────────────────────────────────┐
│ Función moverAdelante (potencia)    │
│ ├─ Poner potencia motorIzq a potencia │
│ └─ Poner potencia motorDer a potencia │
└─────────────────────────────────────┘

// Usar la función
Llamar moverAdelante con potencia 0.7
```

## Hardware en Blocks

### DcMotor (Motores DC)

#### Inicializar Motor

```
Declarar motor como DcMotor "motorName"
Poner dirección motor a FORWARD (o REVERSE)
Poner modo ZeroPower motor a BRAKE (o FLOAT)
Poner modo motor a RUN_USING_ENCODER
```

#### Controlar Motor

```
Poner potencia motor a 0.5          // Rango: -1.0 a 1.0
Obtener potencia motor               // Leer potencia actual
Obtener posición actual motor        // Encoder ticks
Poner posición objetivo motor a 1000 // Para RUN_TO_POSITION
```

#### Modos de Motor

- **RUN_WITHOUT_ENCODER**: Potencia directa, sin feedback
- **RUN_USING_ENCODER**: Control con encoder, más preciso
- **RUN_TO_POSITION**: Mover a posición específica
- **STOP_AND_RESET_ENCODER**: Resetear encoder a 0

### Servo

#### Inicializar Servo

```
Declarar servo como Servo "servoName"
Poner posición servo a 0.5  // Rango: 0.0 a 1.0
```

#### Controlar Servo

```
Poner posición servo a 0.0    // Mínimo
Poner posición servo a 1.0    // Máximo
Poner posición servo a 0.5    // Centro
Obtener posición servo        // Leer posición actual
```

### Sensores

#### Color Sensor

```
Declarar colorSensor como ColorSensor "colorSensor"

// Leer colores
Obtener rojo de colorSensor    // Valor 0-255
Obtener verde de colorSensor
Obtener azul de colorSensor

// Distancia (si tiene sensor integrado)
Obtener distancia de colorSensor en CM
```

#### Distance Sensor

```
Declarar distanceSensor como DistanceSensor "distanceSensor"

Obtener distancia de distanceSensor en CM
Obtener distancia de distanceSensor en INCH
Obtener distancia de distanceSensor en MM
```

#### Touch Sensor (Digital)

```
Declarar touchSensor como DigitalChannel "touchSensor"
Poner modo touchSensor a INPUT

// Leer estado
Si (obtener estado touchSensor)  // true si presionado
  entonces
    // Acción
```

#### IMU (Giroscopio)

```
Declarar imu como BNO055IMU "imu"

// Inicializar con parámetros
Inicializar imu con unidad de ángulo DEGREES

// Obtener orientación
Obtener heading de imu       // Ángulo de rotación (Yaw)
Obtener roll de imu
Obtener pitch de imu
```

### Gamepad

#### Joysticks

```
Obtener joystick Y gamepad1 izquierdo   // Rango: -1.0 (arriba) a 1.0 (abajo)
Obtener joystick X gamepad1 izquierdo   // Rango: -1.0 (izq) a 1.0 (der)
Obtener joystick Y gamepad1 derecho
Obtener joystick X gamepad1 derecho

// Gamepad 2 (operador)
Obtener joystick Y gamepad2 izquierdo
```

**Nota**: El eje Y está invertido (-1 es arriba, 1 es abajo)

#### Botones

```
botón A gamepad1 está presionado
botón B gamepad1 está presionado
botón X gamepad1 está presionado
botón Y gamepad1 está presionado

botón start gamepad1 está presionado
botón back gamepad1 está presionado

dpad arriba gamepad1 está presionado
dpad abajo gamepad1 está presionado
dpad izquierda gamepad1 está presionado
dpad derecha gamepad1 está presionado
```

#### Bumpers y Triggers

```
bumper izquierdo gamepad1 está presionado
bumper derecho gamepad1 está presionado

trigger izquierdo gamepad1   // Valor 0.0 a 1.0
trigger derecho gamepad1     // Valor 0.0 a 1.0
```

### Telemetría

#### Mostrar Datos

```
Telemetry addData clave "Estado" valor "Inicializado"
Telemetry addData clave "Potencia" valor potencia
Telemetry update
```

#### Formato Avanzado

```
// Texto simple
Telemetry addLine "=== MOTORES ==="

// Con formato
Telemetry addData "Voltaje" "%.2f V" voltaje

// Múltiples valores
Telemetry addData "Posición" "X: %.1f, Y: %.1f" x y
```

## Ejemplos Completos

### Ejemplo 1: Drivetrain Tank Drive

```
Ejecutar OpMode
├─ Poner TeleOp
├─ Nombre: "Tank Drive"
│
├─ Llamar Initialize
│  ├─ Declarar frontLeft como DcMotor "frontLeft"
│  ├─ Declarar frontRight como DcMotor "frontRight"
│  ├─ Declarar backLeft como DcMotor "backLeft"
│  ├─ Declarar backRight como DcMotor "backRight"
│  │
│  ├─ Poner dirección frontLeft a REVERSE
│  ├─ Poner dirección backLeft a REVERSE
│  └─ Telemetry addData "Status" "Initialized"
│     Telemetry update
│
├─ Esperar Start
│
└─ Mientras OpModeIsActive
   ├─ Poner leftPower a negar (joystick Y gamepad1 izquierdo)
   ├─ Poner rightPower a negar (joystick Y gamepad1 derecho)
   │
   ├─ Poner potencia frontLeft a leftPower
   ├─ Poner potencia backLeft a leftPower
   ├─ Poner potencia frontRight a rightPower
   ├─ Poner potencia backRight a rightPower
   │
   └─ Telemetry addData "Left" leftPower
      Telemetry addData "Right" rightPower
      Telemetry update
```

### Ejemplo 2: Control de Servo con Botones

```
Ejecutar OpMode
├─ Llamar Initialize
│  ├─ Declarar clawServo como Servo "claw"
│  └─ Poner posición clawServo a 0.5
│
├─ Esperar Start
│
└─ Mientras OpModeIsActive
   ├─ Si (botón A gamepad1 presionado)
   │  entonces
   │    Poner posición clawServo a 0.0  // Cerrar garra
   │
   ├─ Si (botón B gamepad1 presionado)
   │  entonces
   │    Poner posición clawServo a 1.0  // Abrir garra
   │
   └─ Telemetry addData "Servo" obtener posición clawServo
      Telemetry update
```

### Ejemplo 3: Navegación Autónoma Simple

```
Ejecutar OpMode
├─ Poner Autonomous
├─ Nombre: "Auto Adelante"
│
├─ Llamar Initialize
│  ├─ Declarar motor como DcMotor "motor"
│  └─ Poner modo motor a STOP_AND_RESET_ENCODER
│     Poner modo motor a RUN_TO_POSITION
│
├─ Esperar Start
│
└─ // Mover adelante 1000 ticks
   ├─ Poner posición objetivo motor a 1000
   ├─ Poner potencia motor a 0.5
   │
   └─ Mientras (OpModeIsActive Y motor está ocupado)
      └─ Telemetry addData "Posición" obtener posición motor
         Telemetry update
   │
   └─ Poner potencia motor a 0  // Detener
```

### Ejemplo 4: Sensor de Color

```
Ejecutar OpMode
├─ Llamar Initialize
│  ├─ Declarar motor como DcMotor "intake"
│  └─ Declarar colorSensor como ColorSensor "color"
│
├─ Esperar Start
│
└─ Mientras OpModeIsActive
   ├─ Obtener rojo de colorSensor → variable red
   ├─ Obtener azul de colorSensor → variable blue
   │
   ├─ Si (red > blue)  // Objeto rojo detectado
   │  entonces
   │    Poner potencia motor a 1.0  // Intake activado
   │    Telemetry addData "Detectado" "ROJO"
   │  sino si (blue > red)  // Objeto azul
   │    Poner potencia motor a 0
   │    Telemetry addData "Detectado" "AZUL"
   │  sino
   │    Poner potencia motor a 0
   │    Telemetry addData "Detectado" "Ninguno"
   │
   └─ Telemetry update
```

## Consejos y Mejores Prácticas

### Organización de Bloques

1. **Usa comentarios**: Agrega bloques de comentario para explicar secciones
2. **Colapsa bloques**: Haz clic en el ícono `-` para colapsar secciones grandes
3. **Colores**: Los bloques del mismo tipo tienen el mismo color
4. **Alineación**: Arrastra bloques para alinearlos verticalmente

### Debugging

1. **Telemetría abundante**: Muestra valores de variables importantes
2. **Prueba paso a paso**: Desactiva partes del código para aislar problemas
3. **Verifica nombres**: Los nombres en bloques deben coincidir exactamente con configuración de hardware
4. **Observa la consola**: Mensajes de error aparecen al compilar

### Rendimiento

1. **Evita cálculos pesados** en el loop principal
2. **No uses esperas (`wait`)** en TeleOp, causa lag
3. **Actualiza telemetría** cada 5-10 loops, no cada loop
4. **Usa variables** para valores calculados, no recalcules cada vez

### Transición a Java

Cuando estés listo para Java:

1. **Exporta tu OpMode**: Blocks genera código Java que puedes ver
2. **Compara**: Ve cómo tus bloques se traducen a código
3. **Copia**: Usa como referencia para aprender sintaxis Java
4. **Migra gradualmente**: Empieza con Java simple, ve aumentando complejidad

## Limitaciones de Blocks

Blocks es excelente para aprender, pero tiene limitaciones:

### No Soportado en Blocks

- **Librerías externas**: FTCLib, RoadRunner, Pedro Pathing
- **Clases personalizadas**: No puedes crear tus propias clases
- **Algoritmos complejos**: PID avanzado, odometría compleja
- **Computer Vision**: TensorFlow, OpenCV (solo básico)
- **Control de versiones**: Git no es práctico con Blocks

### Cuándo Cambiar a Java

Considera Java cuando:
- Quieras usar librerías avanzadas
- Necesites algoritmos complejos (PID, path following)
- Quieras mejor control y flexibilidad
- Tu equipo tenga experiencia de programación

## Recursos Adicionales

- [Documentación Oficial FTC Blocks](https://ftc-docs.firstinspires.org/)
- [Tutoriales en Video - FIRST YouTube](https://www.youtube.com/c/FIRSTRoboticsCompetition)
- [Game Manual 0](https://gm0.org) - Guía de la comunidad FTC

## Próximos Pasos

- [OnBot Java](./onbot-java.md) - Siguiente nivel de programación
- [Android Studio](./android-studio.md) - Programación avanzada
- [Estructura OpMode](./estructura-opmode.md) - Entender OpModes en profundidad

---

**[← Anterior: Comunicaciones](../02_Sistema_Control/comunicaciones.md)** | **[→ Siguiente: OnBot Java](./onbot-java.md)** | **[↑ Índice](../INTRO_INDICE.md)**
