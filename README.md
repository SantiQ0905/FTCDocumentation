# 📚 Documentación Completa de FTC en Español

Guía integral sobre FIRST Tech Challenge: sistema de control, programación, Sistema Eléctrico, y Librerías Avanzadas.

---

## 📖 ¿Qué encontrarás aquí?

Esta documentación cubre **todos los aspectos esenciales** para competir en FTC, desde los conceptos básicos hasta técnicas avanzadas:

- 🎮 Sistema de control (Control Hub, Driver Station)
- 💻 Programación (Blocks, Java, Android Studio)
- ⚡ Hardware y Sistema Eléctrico
- 📦 Librerías Avanzadas (FTCLib, NextFTC, Pedro Pathing)
- 📝 Ejemplos de código completos
- 🔧 Troubleshooting y mejores prácticas

---

## 🚀 Inicio rápido

### Paso 1: Abre el Índice Principal

**📍 Empieza aquí: [INTRO_INDICE.md](./INTRO_INDICE.md)**

El Índice principal contiene:
- Tabla de contenidos completa con hipervínculos
- Descripción de cada sección
- Enlaces rápidos por nivel de experiencia
- Recursos oficiales y de la comunidad

### Paso 2: Elige tu Ruta de Aprendizaje

####  Nuevo en FTC (Principiante)

Sigue este orden:

1. **¿Qué es FTC?](./01_Introduccion/que-es-ftc.md)** - Entiende el programa y la competencia
2. **[Componentes Básicos](./01_Introduccion/componentes-basicos.md)** - Conoce el Hardware
3. **[Configuración Inicial](./01_Introduccion/configuracion-inicial.md)** - Configura tu primer robot
4. **[Blocks Programming](./03_Programacion/blocks-programming.md)** - Programa sin escribir Código

####  Equipo con Experiencia (Intermedio)

Enfcate en Estás secciones:

1. **[Android Studio](./03_Programacion/android-studio.md)** - Desarrollo profesional
2. **[Conceptos Básicos](./03_Programacion/conceptos-basicos.md)** - PID, state machines, odometría
3. **[FTCLib](./05_FTCLib/introduccion-ftclib.md)** - Librería avanzada
4. **[Pedro Pathing](./07_Pedro_Pathing/introduccion-pedro.md)** - Navegacin autónoma

####  Preparación para Competencia (Todos los niveles)

Revisa Estás secciones críticas:

1. **[Control Hub](./02_Sistema_Control/control-hub.md)** - Configura y diagnostica
2. **[Comunicaciones](./02_Sistema_Control/comunicaciones.md)** - Optimiza Wi-Fi
3. **[Sistema Eléctrico](./04_Sistema_Electrico/alimentación.md)** - Gestán de  Energía
4. **[Driver Station](./02_Sistema_Control/driver-station.md)** - Uso durante partidos

---

## 🧭 Cómo Navegar la Documentación

### Método 1: hipervínculos (Recomendado)

Cada documento incluye enlaces de navegación:

```
[⬅️ Anterior: Documento Previo] | [➡️ Siguiente: Documento Siguiente] | [🏠 Índice]
```

- **⬅️ Anterior**: Vuelve al documento previo
- **➡️ Siguiente**: Avanza al siguiente documento
- **🏠 Índice**: Regresa al Índice principal

### Método 2: Índice Principal

El archivo **[INTRO_INDICE.md](./INTRO_INDICE.md)** contiene hipervínculos a **todos los documentos**, organizados por Categoría.

### Método 3: Búsqueda por Carpeta

Si sabesqué tema buscas:

1. Identifica la carpeta correspondiente (ej. `03_Programacion/`)
2. Abre la carpeta
3. Busca el archivo `.md` relevante

### Método 4: Búsqueda de Texto

Usa la función de Búsqueda de tu editor o visor de Markdown para encontrar términos específicos:

- **VS Code**: `Ctrl+Shift+F` (Windows/Linux) o `Cmd+Shift+F` (Mac)
- **GitHub**: Usa la barra de Búsqueda en el repositorio
- **Obsidian**: `Ctrl+Shift+F` para Búsqueda global

---

## 📑 Contenido por Categoría

### Sistema de Control
- Control Hub (Especificaciones, Configuración, IMU, firmware)
- Expansion Hub (conexión RS485, alimentación)
- Driver Station (interfaz, gamepads, telemetría)
- Comunicaciones (Wi-Fi, optimización, troubleshooting)

### Programación
- **Blocks**: Programación visual para principiantes
- **OnBot Java**: Editor en navegador
- **Android Studio**: IDE profesional
- **Conceptos**: PID, state machines, Odometría, modos de conducción

### Sistema Eléctrico
- Baterías (tipos, carga, distribución)
- Motores (tipos, encoders, modos de control)
- Servos (estándar vs continuo)
- Sensores (color, distancia, IMU, táctil)

### Librerías Avanzadas
- **FTCLib**: Hardware wrappers, PID, command-based
- **NextFTC**: Framework moderno command-based
- **Pedro Pathing**: Path following con curvas de Bézier
- **Recursos Extra**: RoadRunner, EasyOpenCV, FTC Dashboard

---

## 💡 Consejos de Uso

### Para Leer en Computadora

**Editores Recomendados:**
- **VS Code** con extensión "Markdown Preview Enhanced"
- **Obsidian** para vista de gráfico de conocimiento
- **Typora** para edición WYSIWYG
- **GitHub** (visualización web si está en repositorio)

### Para Leer en Tablet/Teléfono

**Apps Recomendadas:**
- **Markor** (Android)
- **iA Writer** (iOS)
- **Obsidian** (iOS/Android)
- Navegador web (si está en GitHub)

### Para Imprimir

Recomendaciones:
- Imprime secciones específicas según necesidad
- Usa vista previa de Markdown para mejor formato
- Considera exportar a PDF primero (VS Code → Markdown PDF)

---

## 🔍 Buscar información Específica

### Por Tema

| Busco información sobre... | Ir a... |
|---------------------------|---------|
| Configurar el Control Hub | [Sistema de Control → Control Hub](./02_Sistema_Control/control-hub.md) |
| Programar en Blocks | [Programación → Blocks](./03_Programacion/blocks-programming.md) |
| Instalar Android Studio | [Programación → Android Studio](./03_Programacion/android-studio.md) |
| Control PID | [Programación → Conceptos Básicos](./03_Programacion/conceptos-basicos.md) |
| Baterías y alimentación | [Sistema Eléctrico → alimentación](./04_Sistema_Electrico/alimentación.md) |
| Usar FTCLib | [FTCLib → Introducción](./05_FTCLib/introduccion-ftclib.md) |
| Path following | [Pedro Pathing → Introducción](./07_Pedro_Pathing/introduccion-pedro.md) |
| Computer visión | [Recursos → EasyOpenCV](./08_Recursos_Adicionales/easycv.md) |

### Por Problema

| Tengo este problema... | Buscar en... |
|----------------------|--------------|
| Robot no conecta | [Comunicaciones](./02_Sistema_Control/comunicaciones.md) |
| Motores no responden | [Sistema Eléctrico → Motores](./04_Sistema_Electrico/motores.md) |
| OpMode no aparece en lista | [Estructura OpMode](./03_Programacion/estructura-opmode.md) |
| Lag en controles | [Comunicaciones](./02_Sistema_Control/comunicaciones.md) o [Conceptos Básicos](./03_Programacion/conceptos-basicos.md) |
| Batería se agota rápido | [alimentación](./04_Sistema_Electrico/alimentación.md) |

---

## 📚 Guías de Estudio Sugeridas

### Plan de 4 Semanas (Principiante)

**Semana 1: Fundamentos**
- Día 1-2: ¿Qué es FTC? + Componentes Básicos
- Día 3-5: Configuración Inicial
- Día 6-7: Blocks Programming (ejemplos Básicos)

**Semana 2: Sistema de Control**
- Día 1-3: Control Hub + Driver Station
- Día 4-5: Comunicaciones
- Día 6-7: Práctica con Hardware real

**Semana 3: Programación**
- Día 1-2: OnBot Java
- Día 3-4: Estructura OpMode
- Día 5-7: Crear OpModes de TeleOp y Autonomous

**Semana 4: Sistema Eléctrico**
- Día 1-2: alimentación + Motores
- Día 3-4: Servos + Sensores
- Día 5-7: Integración completa

### Plan de 2 Semanas (Intermedio/Avanzado)

**Semana 1: Programación Avanzada**
- Día 1-2: Android Studio setup
- Día 3-4: Conceptos Básicos (PID, state machines)
- Día 5-7: FTCLib integration

**Semana 2: navegación Autónoma**
- Día 1-3: Pedro Pathing
- Día 4-5: Odometría
- Día 6-7: Autonomous completo

---

## 🤝 Contribuir

Esta documentación es un recurso educativo. Si encuentras errores o deseas contribuir:

1. Reporta issues o errores
2. Sugiere mejoras
3. Comparte con otros equipos de FTC

---

## ℹ️ información Adicional

### Versión de la Documentación

- **Temporada**: 2025-2026 (DECODE)
- **SDK Versión**: 9.0+
- **Última Actualización**: Diciembre 2025

### Compatibilidad

está Documentación es compatible con:
- Control Hub firmware 1.0+
- FTC SDK 8.0+
- Android Studio 2023.1+
- Java 8+

### Advertencias Importantes

 **Siempre verifica el Game Manual oficial** para:
- Reglas específicas de la temporada actual
- Hardware y software permitido/prohibido
- Restricciones de competencia
- Cambios de último momento

 **Seguridad**: Nunca toques el robot mientras está encendido y en modo RUN

---

## = Enlaces rápidos

### Documentación Oficial
- [FIRST Tech Challenge](https://www.firstinspires.org/programs/ftc/)
- [FTC Docs](https://ftc-docs.firstinspires.org/)
- [Game Manual](https://www.firstinspires.org/resource-library/ftc/game-and-season-info)

### Comunidad
- [Game Manual 0](https://gm0.org)  Altamente recomendado
- [FTC Discord](https://discord.gg/first-tech-challenge)
- [Reddit r/FTC](https://www.reddit.com/r/FTC/)

### Librerías
- [FTCLib](https://docs.ftclib.org/)
- [Pedro Pathing](https://pedropathing.com/)
- [FTC Dashboard](https://acmerobotics.github.io/ftc-dashboard/)

---

##  Soporte

¿Tienes preguntas que no está cubiertas en la Documentación?

1. **Revisa el [Índice Principal](./INTRO_INDICE.md)** -Quizás está en otra seccin
2. **Consulta Game Manual 0** - [gm0.org](https://gm0.org)
3. **Pregunta en FTC Discord** - Comunidad muy activa
4. **Revisa foros oficiales** - Chief Delphi, Reddit

---

##  Comienza Ahora

** [Abre el Índice Principal (INTRO_INDICE.md)](./INTRO_INDICE.md)**

---

<div align="center">

¡Éxito en tu temporada de FTC!** ><

*Documentación creada para equipos de FTC de habla hispana*

</div>

---

## 📄 Licencia

Esta documentación es un recurso educativo compilado de fuentes públicas oficiales de FIRST Tech Challenge y la comunidad FTC.

**Fuentes principales**:
- [FTC Official Documentation](https://ftc-docs.firstinspires.org/)
- [FTCLib Documentation](https://docs.ftclib.org/)
- [Pedro Pathing Documentation](https://pedropathing.com/docs)
- [Game Manual 0](https://gm0.org)

---

*Última Actualización: Diciembre 2025*
