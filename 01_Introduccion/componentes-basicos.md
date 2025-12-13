# Componentes Básicos de un Robot FTC

## Visión General

Un robot FTC está compuesto por varios sistemas integrados que trabajan en conjunto. Esta guía detalla los componentes fundamentales necesarios para construir un robot competitivo.

## 1. Sistema de Control

### Control Hub (REV-31-1595)

El **Control Hub** es el cerebro central del robot FTC moderno.

#### Características Principales

- **Procesador**: Qualcomm Snapdragon 845 (Android)
- **Conectividad**: Wi-Fi Direct integrado
- **Puertos de Motor**: 4 puertos para motores DC
- **Puertos de Servo**: 6 puertos PWM para servos
- **Puertos de Sensor**:
  - 4 puertos I2C
  - 8 puertos Digital I/O
  - 4 puertos Analógicos
- **IMU Integrada**: Sensor de orientación de 9 ejes
- **Batería**: Conector XT30 para batería de 12V

#### Ventajas

- Todo en uno: no requiere teléfono Android separado
- Menor complejidad de cableado
- Mayor confiabilidad
- IMU integrada de alta calidad

### Expansion Hub (REV-31-1153)

El **Expansion Hub** amplía las capacidades del Control Hub.

#### Uso Típico

- Conectado vía cable RS485 al Control Hub
- Proporciona puertos adicionales para motores y sensores
- Útil para robots complejos con muchos actuadores

#### Especificaciones

- Mismos puertos que el Control Hub
- No requiere teléfono Android
- Depende del Control Hub para procesamiento

### Driver Station

Dispositivo Android (teléfono o tablet) usado por los conductores.

#### Funciones

- Interfaz de usuario para iniciar/detener OpModes
- Conexión de hasta 2 gamepads
- Monitoreo de telemetría
- Visualización de errores y advertencias

#### Requisitos

- Android 6.0 (Marshmallow) o superior
- App "Driver Station" instalada desde Google Play o GitHub
- Conexión Wi-Fi Direct al Control Hub

## 2. Sistema de Alimentación

### Batería Principal

#### Especificaciones Permitidas

- **Voltaje**: 12V nominal (3S LiPo o NiMH permitidas)
- **Tipo Recomendado**: Batería REV Robotics (REV-31-1302)
  - Capacidad: 3000mAh
  - Tipo: NiMH
  - Conector: Tamiya convertido a XT30
- **Alternativa**: Batería Matrix (Anderson Powerpole convertido a XT30)

#### Consideraciones de Seguridad

- Nunca cortocircuitar la batería
- Almacenar a temperatura ambiente
- Cargar solo con cargadores aprobados
- Inspeccionar regularmente por daños

### Gestión de Energía

#### Interruptor Principal

- **Requerido**: Switch ON/OFF accesible
- **Ubicación**: Fácil acceso desde el exterior del robot
- **Tipo**: Interruptor de alta corriente (min. 20A)

#### Distribución de Corriente

- Control Hub: hasta 15A total
- Cada motor: hasta 10A continuo (15A pico)
- Servos: corriente combinada no debe exceder límites del puerto

## 3. Motores

### Tipos de Motores Permitidos

#### 1. Motores DC con Encoders

Los más comunes en FTC:

**REV HD Hex Motor (REV-41-1291)**
- Velocidad libre: 6000 RPM (sin caja de cambios)
- Torque de pérdida: 3.2 N·m
- Encoder: Integrado, 28 pulsos por revolución (PPR)
- Uso: Ideal para chasises de alta velocidad con reducción externa

**REV Core Hex Motor (REV-41-1300)**
- Velocidad libre: 125 RPM (con reducción 72:1 integrada)
- Torque de pérdida: 1.9 N·m
- Encoder: Integrado, pulsos por revolución ajustados por reducción
- Uso: Mecanismos que requieren torque y control de velocidad

**goBILDA Yellow Jacket Motors**
- Disponibles en múltiples relaciones de reducción (1620, 435, 312, 223, 117, 84, 60, 50, 30, 19.2, 13.7, 5.2)
- Torque y velocidad variables según reducción
- Encoder integrado
- Uso: Versatilidad para diferentes aplicaciones

#### 2. Motores Especializados

**Motores TETRIX, Actobotics, AndyMark**
- Diversos modelos permitidos según reglas del juego
- Consultar Game Manual 1 para lista completa

### Especificaciones de Cableado

- **Conectores**: Conectores JST VH para motores REV
- **Longitud de Cable**: Minimizar pero permitir movimiento completo
- **Gestión**: Usar amarres de cable y canaletas

## 4. Servos

### Servos Estándar

#### Características

- **Rango de Movimiento**: Típicamente 180° o 270°
- **Control**: Señal PWM desde Control/Expansion Hub
- **Voltaje**: 5V o 6V según modelo
- **Torque**: Variable (desde 3 kg·cm hasta 25+ kg·cm)

#### Modelos Comunes

**goBILDA Dual Mode Servo (2000 Series)**
- Torque: 17.5 kg·cm @ 6V
- Velocidad: 0.14 seg/60° @ 6V
- Modo programable: Servo estándar o continuo

**REV Smart Servo (SRS)**
- Torque: 11.5 kg·cm @ 6V
- Programable vía I2C
- Feedback de posición

### Servos Continuos

#### Uso

- Rotación continua en lugar de posición fija
- Control de velocidad y dirección
- Ideal para rodillos, intakes

#### Ejemplos

- Futaba S148
- REV Servo (modo continuo)
- goBILDA Dual Mode (en modo continuo)

## 5. Sensores

### Sensores de Color

**REV Color Sensor V3 (REV-31-1557)**

#### Capacidades

- Detección de color RGB
- Sensor de distancia/proximidad integrado
- Conexión I2C
- Rango: 1-10cm para detección de distancia

#### Usos Comunes

- Detección de elementos de juego por color
- Sensado de líneas para navegación
- Confirmación de posesión de objetos

### Sensores de Distancia

**REV 2m Distance Sensor (REV-31-1505)**

#### Especificaciones

- Rango: 10mm a 2000mm
- Precisión: ±1% del rango
- Conexión: I2C o Digital
- Tiempo de respuesta: <10ms

#### Aplicaciones

- Navegación autónoma
- Detección de paredes y obstáculos
- Alineación precisa

**Sensores Ultrasónicos**
- Alternativa para detección de rango
- Menos precisos que Time-of-Flight
- Más económicos

### Sensores Táctiles y Magnéticos

**REV Touch Sensor (REV-31-1425)**

- Detección de contacto físico
- Switch normalmente abierto
- Útil para límites de mecanismos

**REV Magnetic Limit Switch**

- Detección sin contacto
- Mayor durabilidad que switches mecánicos
- Requiere imán permanente

### IMU (Inertial Measurement Unit)

**REV IMU (integrada en Control Hub)**

#### Componentes

- Acelerómetro de 3 ejes
- Giroscopio de 3 ejes
- Magnetómetro de 3 ejes

#### Aplicaciones

- Navegación autónoma con orientación precisa
- Estabilización de mecanismos
- Detección de colisiones
- Odometría complementaria

## 6. Cámaras y Visión por Computadora

### Opciones de Cámara

**Logitech C920/C270**

- USB, conecta directamente al Control Hub
- Resolución HD
- Compatible con EasyOpenCV y Vuforia

**Webcams Genéricas**

- Muchas webcams USB funcionan
- Verificar compatibilidad con Android

### Frameworks de Visión

- **Vuforia**: Reconocimiento de objetivos pre-definidos
- **TensorFlow Lite**: Detección de objetos con modelos entrenados
- **EasyOpenCV**: Pipelines personalizados para procesamiento de imágenes
- **EOCV-Sim**: Simulador para desarrollar pipelines sin robot físico

## 7. Estructura y Chasis

### Sistemas de Construcción Permitidos

#### REV Robotics

- Extrusions de 15mm y 45mm
- Pattern de agujeros compatible con M3
- goBILDA compatible parcialmente

#### goBILDA

- Sistema métrico basado en patrón de 8mm
- Amplia variedad de componentes
- Excelente ecosistema de motion y estructura

#### TETRIX

- Sistema basado en canales de aluminio
- Tornillos y conectores especializados
- Compatible con LEGO parcialmente

#### Actobotics

- Sistema de ServoCity
- Hub pattern y canales
- Gran variedad de componentes de motion

### Ruedas y Tracción

#### Tipos de Ruedas

**Mecanum**
- Movimiento omnidireccional
- 4 ruedas con rodillos a 45°
- Mayor maniobrabilidad, menor tracción

**Omni**
- Movimiento lateral sin rotación del robot
- Rodillos perpendiculares al eje de la rueda
- Configuraciones H-drive, X-drive

**Tracción Estándar**
- Mayor tracción y empuje
- Movimiento solo hacia adelante/atrás y giro
- Más simple de programar

## 8. Gamepad/Controladores

### Controladores Permitidos

- **Logitech F310**: Muy común, económico
- **Xbox 360 Controller**: Inalámbrico disponible
- **PS4 Controller**: Compatible vía USB o Bluetooth
- **Xbox One Controller**: Compatible

### Configuración

- Hasta 2 gamepads por Driver Station
- Emparejamiento vía Bluetooth o USB
- Mapeo de botones personalizable en código

## 9. Cables y Conectores

### Tipos de Cables

#### Cables de Motor

- JST VH de 2 pines
- AWG apropiado para corriente (mín. 18 AWG)
- Longitudes: 300mm, 450mm, 600mm comunes

#### Cables de Servo

- JST PH de 3 pines (señal, VCC, GND)
- 22-24 AWG típico
- Extensiones disponibles

#### Cables de Sensor

**I2C**: 4 pines (GND, VCC, SDA, SCL)
**Digital**: 4 pines para sensores digitales
**Analog**: 3 pines para sensores analógicos

### Gestión de Cables

- **Amarres de Cable**: Organización y prevención de enredos
- **Canaletas**: Protección de cables en áreas de movimiento
- **Etiquetado**: Identificación clara de cada cable
- **Longitud Apropiada**: No demasiado tensos ni excesivamente largos

## 10. Herramientas Esenciales

### Herramientas Mecánicas

- Llaves Allen (métrico e imperial)
- Destornilladores Phillips y planos
- Pinzas de punta fina
- Cortadores de cable
- Taladro y brocas
- Sierra de metales
- Limas

### Herramientas Eléctricas

- Multímetro
- Pelacables
- Herramienta de crimpar
- Soldador (para proyectos avanzados)
- Pistola de pegamento caliente

### Herramientas de Programación

- Laptop con Android Studio
- Cable USB para conectar al Control Hub
- Driver Station (teléfono/tablet)
- Cargadores para dispositivos

## Próximos Pasos

Para configurar estos componentes:

- [Configuración Inicial](./configuracion-inicial.md) - Conectar y configurar componentes
- [Sistema de Control](../02_Sistema_Control/control-hub.md) - Configuración detallada del Control Hub
- [Sistema Eléctrico](../04_Sistema_Electrico/alimentacion.md) - Cableado y conexiones eléctricas

---

**[← Volver al Índice](../INTRO_INDICE.md)** | **[→ Siguiente: Configuración Inicial](./configuracion-inicial.md)**
