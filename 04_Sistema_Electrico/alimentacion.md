# Sistema de Alimentación FTC

## Baterías

### Tipos Permitidos

**NiMH (Recomendado)**
- Voltaje: 12V nominal
- Capacidad típica: 3000mAh
- Modelo REV: REV-31-1302
- Seguras, durables, permitidas en competencia

**LiPo (Permitido con restricciones)**
- 3S (11.1V nominal, 12.6V cargado)
- Verificar Game Manual para restricciones
- Mayor densidad energética
- Requiere cargador especial

### Conectores

- **XT30**: Estándar para Control Hub
- **Tamiya**: Común en baterías NiMH (convertir a XT30)
- **Anderson Powerpole**: Usados en distribución

### Carga de Baterías

**NiMH**:
```
Cargador REV: 1-2 horas carga completa
Voltaje completo: 12.8-13.2V
Voltaje descargado: <11V
```

**Mejores Prácticas**:
- Cargar noche antes de competencia
- Nunca almacenar completamente descargadas
- Verificar voltaje con multímetro antes de usar
- Llevar mínimo 2 baterías cargadas a competencias

## Distribución de Energía

### Configuración Básica

```
[Batería 12V] ─── [Interruptor] ─── [XT30] ─── [Control Hub]
                                                      │
                                                   Motores
                                                   Servos
                                                   Sensores
```

### Con Expansion Hub

```
[Batería 1] ───► [Control Hub] ───► Drivetrain

[Batería 2] ───► [Expansion Hub] ─►  Mecanismos
       │                                          │
       └──────────► [RS485] ◄───────────────────┘
```

## Gestión de Corriente

### Límites de Corriente

- **Control Hub Total**: 50A (fusible auto-reseteable)
- **Por Motor**: 10A continuo, 15A pico
- **Servos Totales**: 6A compartidos
- **Lógica**: 20A (fusible separado)

### Cálculo de Consumo

```java
Drivetrain (4 motores): 4 × 10A = 40A pico
Mecanismos (2 motores): 2 × 10A = 20A pico
Servos (3 servos): ~3A
Total: ~63A pico (excede 50A de fusible)
```

**Solución**: Nunca acelerar todos los motores simultáneamente al 100%

### Código para Ramping

```java
// Ramping gradual de potencia
public double rampPower(double targetPower, double currentPower, double rampRate) {
    if (Math.abs(targetPower - currentPower) < rampRate) {
        return targetPower;
    }
    if (targetPower > currentPower) {
        return currentPower + rampRate;
    } else {
        return currentPower - rampRate;
    }
}

// Uso
double currentPower = 0;
while (opModeIsActive()) {
    double targetPower = gamepad1.left_stick_y;
    currentPower = rampPower(targetPower, currentPower, 0.05);
    motor.setPower(currentPower);
}
```

## Cableado

### Gauge de Cables

- **Motores**: 18-20 AWG
- **Servos**: 22-24 AWG
- **Batería principal**: 14-16 AWG

### Gestión de Cables

1. **Organización**: Amarres de cable, canaletas
2. **Etiquetado**: Marcar cada cable (motor, sensor, etc.)
3. **Routing**: Separar cables de potencia de señal
4. **Longitud**: Minimizar pero permitir movimiento completo
5. **Protección**: Evitar bordes afilados, partes móviles

## Troubleshooting

### Voltaje Bajo

**Síntomas**: Robot lento, reinicios, desconexiones

**Soluciones**:
- Cargar/reemplazar batería
- Verificar conexiones XT30 firmes
- Reducir carga simultánea

### Motores No Responden

**Diagnóstico**:
1. Verificar voltaje batería >12V
2. Probar motor en diferente puerto
3. Verificar cable del motor
4. Verificar fusible del Control Hub (contactar REV si falla)

---

**[↑ Índice](../INTRO_INDICE.md)**
