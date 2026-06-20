# SnowPro Core COF-C03 — Recursos de Estudio

<p align="center">
  <img src="https://img.shields.io/badge/Estado-Activo-22c55e?style=flat-square" alt="Estado: Activo">
  <img src="https://img.shields.io/badge/Examen-COF--C03-3b82f6?style=flat-square" alt="Examen COF-C03">
  <img src="https://img.shields.io/badge/Idioma-Español-ef4444?style=flat-square" alt="Idioma Español">
  <img src="https://img.shields.io/badge/Archivos-35-6b7280?style=flat-square" alt="35 archivos">
  <img src="https://img.shields.io/badge/Días-46-eab308?style=flat-square" alt="46 días">
  <img src="https://img.shields.io/badge/Horas-60-a855f7?style=flat-square" alt="60 horas">
</p>

> Repositorio completo de estudio para la certificación **SnowPro Core (COF-C03)**.
> Incluye apuntes teóricos, guías DORA prácticas, calendario interactivo, plan de estudio, tutorial para principiantes y 30 preguntas tipo examen.

## Estructura del repositorio

```
📁 01_Arquitectura/          → 5 archivos (arquitectura 3 capas, microparticiones, warehouses, tablas)
📁 02_Gobernanza/            → 10 archivos (RBAC, masking, network policies, resource monitors, cifrado)
📁 03_Carga_Descarga/        → 2 archivos (carga estructurada/semiestructurada, datos no estructurados)
📁 04_Optimizacion/          → (contenido cubierto en archivos generales)
📁 05_Colaboracion/          → 3 archivos (Data Sharing, Data Clean Rooms, Marketplace)
📁 General/                   → 15 archivos + imágenes (apuntes maestros, guías, tutorial, plan horario, informe)
```

## Cómo usar este material

### 1. Por tema (recomendado)

Usa [`General/guia_dora_badges.md`](General/guia_dora_badges.md) — organizado por cada tema del examen, indica:
- Qué insignia DORA lo practica
- Dónde estudiarlo (archivo + sección)
- Sintaxis SQL clave
- Práctica recomendada

### 2. Por calendario

Abre [`index.html`](index.html) — calendario interactivo con plan día por día (1 jul – 15 ago 2026, 46 días, 60h).

### 3. Por archivo guía

| Archivo | Qué contiene |
|---|---|
| [`General/apuntes_snowpro_core.md`](General/apuntes_snowpro_core.md) | Apuntes completos de los 5 dominios + preguntas frecuentes + apéndices |
| [`General/guia_completa_COF-C03.md`](General/guia_completa_COF-C03.md) | Mapeo dominio ↔ material existente + plan 30 días + checklist |
| [`General/informe_snowflake.md`](General/informe_snowflake.md) | 30 preguntas tipo examen con respuestas y explicaciones |
| [`General/plan_estudio_snowpro_core.md`](General/plan_estudio_snowpro_core.md) | 21 temas extendidos NO cubiertos en las 30 preguntas |
| [`General/plan_horario_detallado.md`](General/plan_horario_detallado.md) | Cronograma día por día (30 días, 60 horas totales) |
| [`General/Tutorial Snowflake - Principiante a Experto.md`](General/Tutorial%20Snowflake%20-%20Principiante%20a%20Experto.md) | Tutorial completo desde cero |

### 4. Por dominio

Cada carpeta de dominio contiene archivos dedicados a ese tema específico del examen SnowPro Core.

## Distribución del examen

| Dominio | % | Preguntas |
|---|---|---|
| 1. Arquitectura y características | 31% | ~31 |
| 2. Gestión de cuentas y gobernanza | 20% | ~20 |
| 3. Carga, descarga y conectividad | 18% | ~18 |
| 4. Optimización y transformación | 21% | ~21 |
| 5. Colaboración de datos | 10% | ~10 |

## Badges DORA (práctica hands-on)

Los talleres DORA son laboratorios gratuitos en [learn.snowflake.com](https://learn.snowflake.com/).
Cada insignia cubre distintos temas del examen. La ruta recomendada:

1. **Insignia 1** — Data Warehousing (~40% del examen)
2. **Insignia 2** — Collaboration, Marketplace & Cost (~15%)
3. **Insignia 5** — Data Engineering (~25%)

## Licencia

Este material es de uso personal y educativo. Basado en la documentación oficial de Snowflake y el contenido de DataCamp.
