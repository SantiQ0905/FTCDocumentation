# Estructura de OpModes en FTC

## ¿Qué es un OpMode?

Un **OpMode** (Operation Mode) es un programa que controla el robot durante una fase específica del partido. Existen dos tipos principales:

- **TeleOp**: Controlado por humanos con gamepads (2 min)
- **Autonomous**: El robot opera completamente solo (30 seg)

## Tipos de OpMode

### 1. LinearOpMode

El tipo más común y recomendado para comenzar.

#### Características

- Código ejecuta secuencialmente de arriba hacia abajo
- Usa `waitForStart()` para esperar inicio
- Loop principal con `while (opModeIsActive())`
- Más intuitivo y fácil de entender

#### Estructura Básica

```java
@TeleOp(name="Ejemplo Linear", group="Linear")
public class EjemploLinear extends LinearOpMode {

    @Override
    public void runOpMode() {
        // 1. INICIALIZACIÓN
        // Ejecuta una vez al presionar INIT

        // 2. ESPERAR START
        waitForStart();

        // 3. LOOP PRINCIPAL
        // Ejecuta repetidamente mientras OpMode está activo
        while (opModeIsActive()) {
            // Tu código aquí
        }

        // 4. LIMPIEZA (Opcional)
        // Ejecuta al terminar
    }
}
```

#### Ejemplo Completo

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.util.ElapsedTime;

@TeleOp(name="Linear TeleOp", group="Linear")
public class LinearTeleOp extends LinearOpMode {

    // Hardware
    private DcMotor leftDrive = null;
    private DcMotor rightDrive = null;

    // Variables
    private ElapsedTime runtime = new ElapsedTime();

    @Override
    public void runOpMode() {
        // === INICIALIZACIÓN ===
        telemetry.addData("Status", "Inicializando...");
        telemetry.update();

        leftDrive = hardwareMap.get(DcMotor.class, "left_drive");
        rightDrive = hardwareMap.get(DcMotor.class, "right_drive");

        leftDrive.setDirection(DcMotor.Direction.FORWARD);
        rightDrive.setDirection(DcMotor.Direction.REVERSE);

        telemetry.addData("Status", "Initialized");
        telemetry.update();

        // === ESPERAR START ===
        waitForStart();
        runtime.reset();

        // === LOOP PRINCIPAL ===
        while (opModeIsActive()) {
            // Leer gamepad
            double leftPower = -gamepad1.left_stick_y;
            double rightPower = -gamepad1.right_stick_y;

            // Aplicar potencia
            leftDrive.setPower(leftPower);
            rightDrive.setPower(rightPower);

            // Telemetría
            telemetry.addData("Status", "Run Time: " + runtime.toString());
            telemetry.addData("Motors", "left (%.2f), right (%.2f)",
                             leftPower, rightPower);
            telemetry.update();
        }
    }
}
```

### 2. OpMode (Iterativo)

Tipo avanzado basado en callbacks/métodos.

#### Características

- Basado en métodos `init()`, `start()`, `loop()`, etc.
- No usa bucles explícitos
- SDK llama métodos automáticamente
- Más flexible para arquitecturas complejas

#### Estructura Básica

```java
@TeleOp(name="Ejemplo Iterativo", group="Iterativo")
public class EjemploIterativo extends OpMode {

    @Override
    public void init() {
        // Ejecuta una vez al presionar INIT
    }

    @Override
    public void init_loop() {
        // Ejecuta repetidamente después de init() hasta START
    }

    @Override
    public void start() {
        // Ejecuta una vez al presionar START
    }

    @Override
    public void loop() {
        // Ejecuta repetidamente mientras OpMode está activo
        // ¡Este es el "loop principal"!
    }

    @Override
    public void stop() {
        // Ejecuta una vez al presionar STOP
    }
}
```

#### Ejemplo Completo

```java
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.OpMode;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.util.ElapsedTime;

@TeleOp(name="Iterativo TeleOp", group="Iterativo")
public class IterativoTeleOp extends OpMode {

    private DcMotor leftDrive;
    private DcMotor rightDrive;
    private ElapsedTime runtime = new ElapsedTime();

    @Override
    public void init() {
        telemetry.addData("Status", "Inicializando...");

        leftDrive = hardwareMap.get(DcMotor.class, "left_drive");
        rightDrive = hardwareMap.get(DcMotor.class, "right_drive");

        leftDrive.setDirection(DcMotor.Direction.FORWARD);
        rightDrive.setDirection(DcMotor.Direction.REVERSE);

        telemetry.addData("Status", "Initialized");
    }

    @Override
    public void init_loop() {
        telemetry.addData("Status", "Esperando START...");
    }

    @Override
    public void start() {
        runtime.reset();
    }

    @Override
    public void loop() {
        double leftPower = -gamepad1.left_stick_y;
        double rightPower = -gamepad1.right_stick_y;

        leftDrive.setPower(leftPower);
        rightDrive.setPower(rightPower);

        telemetry.addData("Status", "Run Time: " + runtime.toString());
        telemetry.addData("Motors", "left (%.2f), right (%.2f)",
                         leftPower, rightPower);
    }

    @Override
    public void stop() {
        leftDrive.setPower(0);
        rightDrive.setPower(0);
        telemetry.addData("Status", "Stopped");
        telemetry.update();
    }
}
```

## Ciclo de Vida de un OpMode

### LinearOpMode

```
[INIT presionado]
        ↓
    runOpMode() comienza
        ↓
    Inicialización
        ↓
    waitForStart() - ESPERA
        ↓
[START presionado]
        ↓
    while (opModeIsActive())
        ├→ Código del loop
        ├→ Repite
        └→ opModeIsActive() == false
                ↓
[STOP presionado o termina tiempo]
        ↓
    Código después del while (opcional)
        ↓
    OpMode termina
```

### OpMode (Iterativo)

```
[INIT presionado]
        ↓
    init() ejecuta una vez
        ↓
    init_loop() ejecuta repetidamente
        ↓
[START presionado]
        ↓
    start() ejecuta una vez
        ↓
    loop() ejecuta repetidamente
        ↓
[STOP presionado]
        ↓
    stop() ejecuta una vez
        ↓
    OpMode termina
```

## Anotaciones

### @TeleOp

Marca un OpMode como TeleOp (controlado por humano).

```java
@TeleOp(name="Nombre Mostrado", group="Categoría")
public class MiTeleOp extends LinearOpMode {
    // ...
}
```

**Parámetros**:
- `name`: Nombre mostrado en Driver Station
- `group`: Categoría para organizar OpModes

### @Autonomous

Marca un OpMode como Autónomo.

```java
@Autonomous(name="Auto Rojo", group="Autonomous")
public class AutoRojo extends LinearOpMode {
    // ...
}
```

**Parámetros**:
- `name`: Nombre mostrado
- `group`: Categoría
- `preselectTeleOp` (opcional): OpMode TeleOp a cargar después

```java
@Autonomous(name="Auto", preselectTeleOp="TeleOp Principal")
```

### @Disabled

Oculta un OpMode de la lista en Driver Station.

```java
@Disabled
@TeleOp(name="OpMode en Desarrollo", group="Test")
public class OpModeEnDesarrollo extends LinearOpMode {
    // No aparecerá en la lista
}
```

**Uso**: Para OpModes en desarrollo o deprecated.

## Elementos Clave

### hardwareMap

Objeto que proporciona acceso al hardware configurado.

```java
// Obtener motor
DcMotor motor = hardwareMap.get(DcMotor.class, "motor_name");

// Obtener servo
Servo servo = hardwareMap.get(Servo.class, "servo_name");

// Obtener sensor
ColorSensor colorSensor = hardwareMap.get(ColorSensor.class, "color");
```

**Importante**: El nombre ("motor_name") debe coincidir EXACTAMENTE con la configuración de hardware.

### telemetry

Objeto para enviar datos al Driver Station.

```java
// Agregar datos
telemetry.addData("Clave", "Valor");
telemetry.addData("Número", 123);
telemetry.addData("Decimal", "%.2f", 3.14159);

// Agregar línea sin clave
telemetry.addLine("Esta es una línea de texto");

// IMPORTANTE: Llamar update() para enviar
telemetry.update();
```

### gamepad1 y gamepad2

Objetos para leer entrada de gamepads.

```java
// Joysticks (-1.0 a 1.0)
double leftY = gamepad1.left_stick_y;
double rightX = gamepad1.right_stick_x;

// Botones (true/false)
boolean buttonA = gamepad1.a;
boolean dpadUp = gamepad1.dpad_up;

// Triggers (0.0 a 1.0)
double leftTrigger = gamepad1.left_trigger;

// Bumpers (true/false)
boolean leftBumper = gamepad1.left_bumper;
```

### opModeIsActive()

Método que verifica si el OpMode sigue activo.

```java
while (opModeIsActive()) {
    // Loop continúa mientras:
    // - No se presione STOP
    // - No se alcance límite de tiempo
    // - No haya error crítico
}
```

**Importante**: Solo disponible en LinearOpMode.

### waitForStart()

Pausa ejecución hasta que se presione START.

```java
// Inicialización
// ...

waitForStart();  // Espera aquí

// Código después de START
```

### sleep()

Pausa ejecución por tiempo específico (milisegundos).

```java
sleep(1000);  // Espera 1 segundo (1000 ms)
```

**Advertencia**: `sleep()` bloquea completamente el OpMode. Evita en TeleOp.

### ElapsedTime

Clase para medir tiempo transcurrido.

```java
import com.qualcomm.robotcore.util.ElapsedTime;

ElapsedTime timer = new ElapsedTime();

// Resetear temporizador
timer.reset();

// Obtener tiempo transcurrido
double seconds = timer.seconds();
double milliseconds = timer.milliseconds();

// Usar en timeout
while (opModeIsActive() && timer.seconds() < 5.0) {
    // Ejecuta por máximo 5 segundos
}
```

## Patrones Comunes

### Autonomous con Timeouts

```java
@Autonomous(name="Auto con Timeout", group="Auto")
public class AutoTimeout extends LinearOpMode {

    private DcMotor motor;
    private ElapsedTime runtime = new ElapsedTime();

    @Override
    public void runOpMode() {
        motor = hardwareMap.get(DcMotor.class, "motor");

        waitForStart();
        runtime.reset();

        // Mover adelante por 3 segundos
        motor.setPower(0.5);
        while (opModeIsActive() && runtime.seconds() < 3.0) {
            telemetry.addData("Time", runtime.seconds());
            telemetry.update();
        }

        // Detener
        motor.setPower(0);
    }
}
```

### TeleOp con State Machine

```java
@TeleOp(name="TeleOp State Machine", group="TeleOp")
public class TeleOpStateMachine extends LinearOpMode {

    enum State {
        MANUAL,
        AUTO_PICKUP,
        AUTO_PLACE
    }

    private State currentState = State.MANUAL;
    private DcMotor motor;

    @Override
    public void runOpMode() {
        motor = hardwareMap.get(DcMotor.class, "motor");

        waitForStart();

        while (opModeIsActive()) {
            switch (currentState) {
                case MANUAL:
                    motor.setPower(gamepad1.left_stick_y);
                    if (gamepad1.a) {
                        currentState = State.AUTO_PICKUP;
                    }
                    break;

                case AUTO_PICKUP:
                    // Lógica de pickup automático
                    motor.setPower(0.5);
                    sleep(1000);
                    currentState = State.MANUAL;
                    break;

                case AUTO_PLACE:
                    // Lógica de colocación automática
                    break;
            }

            telemetry.addData("State", currentState);
            telemetry.update();
        }
    }
}
```

## LinearOpMode vs OpMode: ¿Cuál Usar?

### Usa LinearOpMode si:
- ✅ Estás comenzando con FTC
- ✅ Tu código es mayormente secuencial
- ✅ Autonomous simples (mover → girar → mover)
- ✅ Prefieres código más legible

### Usa OpMode (Iterativo) si:
- ✅ Necesitas arquitectura compleja
- ✅ Usas State Machines elaboradas
- ✅ Necesitas control preciso sobre cada fase
- ✅ Quieres evitar bucles bloqueantes

**Recomendación General**: LinearOpMode para 90% de casos.

## Próximos Pasos

- [Conceptos Básicos](./conceptos-basicos.md) - Algoritmos y técnicas
- [FTCLib](../05_FTCLib/introduccion-ftclib.md) - Usar command-based programming

---

**[← Anterior: Android Studio](./android-studio.md)** | **[→ Siguiente: Conceptos Básicos](./conceptos-basicos.md)** | **[↑ Índice](../INTRO_INDICE.md)**
