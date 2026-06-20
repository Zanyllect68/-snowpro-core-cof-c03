# Guía Completa SnowPro Core — COF-C03

## Datos del Examen

| Aspecto | Detalle |
|---|---|
| **Versión** | COF-C03 |
| **Total preguntas** | 100 |
| **Tipo** | Selección múltiple, múltiples opciones |
| **Tiempo** | 115 minutos |
| **Idiomas** | Inglés, japonés, coreano, francés, español |
| **Costo** | $175 USD ($140 USD India) |
| **Aprobación** | 750/1000 |
| **Prerrequisitos** | Ninguno |
| **Entrega** | Online supervisado o centros presenciales |

---

## Mapeo Completo: Dominios vs Material Existente

### Dominio 1.0 — Características y Arquitectura de Snowflake AI Data Cloud (31%)
**Peso más alto del examen — Prioridad #1**

| Sub-tema | Dónde estudiarlo |
|---|---|
| Arquitectura multicapa (Cloud Services, Compute, Storage) | `plan_estudio_snowpro_core.md` — Secc. 1 y 4 |
| Microparticiones y clustering | `plan_estudio_snowpro_core.md` — Secc. 1 |
| Time Travel y Fail-safe | `plan_estudio_snowpro_core.md` — Secc. 4, `informe_snowflake.md` — Preg. 04, 16 |
| Zero-copy cloning | `plan_estudio_snowpro_core.md` — Secc. 3 |
| Tipos de tablas (permanente, transitoria, temporal) | `plan_estudio_snowpro_core.md` — Secc. 5 |
| Ediciones de Snowflake (Standard, Enterprise, etc.) | `plan_estudio_snowpro_core.md` — Secc. 8 |
| Seguridad a nivel de objeto (roles, privilegios) | `plan_estudio_snowpro_core.md` — Secc. 11, `informe_snowflake.md` — Preg. 21, 23 |
| Caching (result, metadata, query) | `plan_estudio_snowpro_core.md` — Secc. 2 |
| Snowsight y hojas de trabajo | `informe_snowflake.md` — Preg. 03, 19 |
| Almacenes virtuales (auto-suspend, sizing) | `informe_snowflake.md` — Preg. 05, 22 |
| Notebooks y Cortex AI | `informe_snowflake.md` — Preg. 06, 07, 09, 15, 18, 29 |
| DORA relacionado | **Insignia 1** (Data Warehousing) — cubre warehouse, tablas, cloning, time travel |
| Preguntas del informe que aplican | 03, 04, 05, 06, 07, 09, 10, 11, 13, 14, 15, 16, 21, 22, 23, 27, 29, 30 |

---

### Dominio 2.0 — Gestión de Cuentas y Gobernanza de Datos (20%)
**Segundo peso más alto — Prioridad #2**

| Sub-tema | Dónde estudiarlo |
|---|---|
| Roles del sistema (ACCOUNTADMIN, SYSADMIN, etc.) | `plan_estudio_snowpro_core.md` — Secc. 11, `informe_snowflake.md` — Preg. 23 |
| RBAC y herencia de roles | `plan_estudio_snowpro_core.md` — Secc. 11 |
| Políticas de enmascaramiento (Masking Policies) | `plan_estudio_snowpro_core.md` — Secc. 12 |
| Políticas de acceso a filas (Row Access Policies) | `plan_estudio_snowpro_core.md` — Secc. 12 |
| Políticas de red (Network Policies) | `plan_estudio_snowpro_core.md` — Secc. 12 |
| Resource Monitors | `plan_estudio_snowpro_core.md` — Secc. 7 |
| Data Classification y tagging | `plan_estudio_snowpro_core.md` — Secc. 12 |
| MFA, SSO, OAuth, Key Pair Auth | `plan_estudio_snowpro_core.md` — Secc. 15 |
| Privacidad (HIPAA, HITRUST, etc.) | `plan_estudio_snowpro_core.md` — Secc. 8 (Business Critical) |
| DORA relacionado | **Insignia 2** (Collaboration, Marketplace & Cost) — resource monitors, costos |
| Preguntas del informe que aplican | 05, 22, 23 |

> **⚠️ Atención:** Este dominio tiene solo 3 preguntas en el informe de 30. Las 27 preguntas restantes del examen real se enfocarán en políticas de datos, RBAC, gestion de cuentas, etc. **Necesitas reforzar este dominio con el plan de estudio.**

---

### Dominio 3.0 — Carga y Descarga de Datos y Conectividad (18%)
**Prioridad #3**

| Sub-tema | Dónde estudiarlo |
|---|---|
| COPY INTO (carga desde stage a tabla) | `informe_snowflake.md` — Preg. 02, 12, 17 |
| Stages (user, table, named, interno, externo) | `plan_estudio_snowpro_core.md` — Secc. 6 |
| Formatos de archivo (JSON, Avro, ORC, Parquet, CSV) | `informe_snowflake.md` — Preg. 28, `plan_estudio_snowpro_core.md` — Secc. 17 |
| Datos semiestructurados (VARIANT, FLATTEN) | `informe_snowflake.md` — Preg. 24 |
| Datos no estructurados en stages y PARSE_DOCUMENT | `informe_snowflake.md` — Preg. 20, 25 |
| Conectividad (Private Link, OAuth, ODBC/JDBC) | `plan_estudio_snowpro_core.md` — Secc. 15 |
| Snowpipe (carga automatizada) | *(No cubierto — agregar al plan)* |
| Descarga de datos (COPY INTO location) | *(No cubierto — agregar al plan)* |
| DORA relacionado | **Insignia 4** (Data Lake) — external tables, semiestructurados, stages |
| Preguntas del informe que aplican | 02, 12, 17, 20, 24, 25, 28 |

---

### Dominio 4.0 — Optimización del Rendimiento, Consultas y Transformación (21%)
**Prioridad #2 (empata con Dominio 2)**

| Sub-tema | Dónde estudiarlo |
|---|---|
| Sintaxis SQL (SELECT, LIMIT, WHERE, JOIN) | `informe_snowflake.md` — Preg. 13, 30 |
| Funciones de agregación y ventana | `plan_estudio_snowpro_core.md` — Secc. 18 |
| Clustering y partition pruning | `plan_estudio_snowpro_core.md` — Secc. 1 |
| Search Optimization Service | `plan_estudio_snowpro_core.md` — Secc. 19 |
| EXPLAIN y Query Profile | `plan_estudio_snowpro_core.md` — Secc. 19 |
| Dynamic Tables | `plan_estudio_snowpro_core.md` — Secc. 9 |
| Materialized Views | `plan_estudio_snowpro_core.md` — Secc. 9 |
| Tasks y Streams | `plan_estudio_snowpro_core.md` — Secc. 10 |
| CTEs y subconsultas | *(No cubierto explícitamente)* |
| DORA relacionado | **Insignia 5** (Data Engineering) — dynamic tables, streams, tasks, clustering |
| Preguntas del informe que aplican | 13, 30 |

---

### Dominio 5.0 — Colaboración de Datos (10%)
**Peso más bajo — Prioridad #4**

| Sub-tema | Dónde estudiarlo |
|---|---|
| Secure Data Sharing | `plan_estudio_snowpro_core.md` — Secc. 20 |
| Reader Accounts | `plan_estudio_snowpro_core.md` — Secc. 20 |
| Snowflake Marketplace | `informe_snowflake.md` — Preg. 08 |
| Data Exchange | `informe_snowflake.md` — Preg. 08 |
| Private Data Exchange | `plan_estudio_snowpro_core.md` — Secc. 20 |
| Auto-fulfillment | `plan_estudio_snowpro_core.md` — Secc. 20 |
| Listings (público, privado, personalizado) | *(No cubierto explícitamente)* |
| DORA relacionado | **Insignia 2** (Collaboration, Marketplace & Cost) |
| Preguntas del informe que aplican | 08 |

---

## Distribución estimada de preguntas por dominio

| Dominio | % | Preguntas estimadas (de 100) | Cubiertas en informe 30 preg. |
|---|---|---|---|
| 1.0 Arquitectura | 31% | ~31 | 18 preg. |
| 2.0 Gestión de cuentas | 20% | ~20 | 3 preg. |
| 3.0 Carga/descarga | 18% | ~18 | 7 preg. |
| 4.0 Optimización y consultas | 21% | ~21 | 2 preg. |
| 5.0 Colaboración | 10% | ~10 | 1 preg. |

**Conclusión:** Las 30 preguntas del informe cubren bien el Dominio 1 y parcialmente el 3. Los Dominios 2 y 4 están subrepresentados. El Dominio 5 está apenas tocado.

**Debes enfocar tu estudio extra en:**
1. **Dominio 2** (gestión de cuentas y gobernanza) — 20 preguntas, solo 3 cubiertas
2. **Dominio 4** (optimización y transformación) — 21 preguntas, solo 2 cubiertas
3. **Dominio 5** (colaboración) — 10 preguntas, solo 1 cubierta

---

## Plan de estudio cronológico (30 días)

| Semana | Días | Dominio | Actividad | Material |
|---|---|---|---|---|
| **Semana 1** | 1-3 | 1.0 (31%) | Leer y practicar | `informe_snowflake.md` + Dominio 1 del plan |
| | 4-5 | 1.0 | Laboratorio DORA | **Insignia 1** (Data Warehousing) |
| | 6-7 | 1.0 | Repaso y práctica | Refuerza microparticiones, arquitectura, caching |
| **Semana 2** | 8-9 | 3.0 (18%) | Leer y practicar | Stages, COPY INTO, formatos, FLATTEN, PARSE_DOCUMENT |
| | 10-11 | 3.0 | Laboratorio DORA | **Insignia 4** (Data Lake) |
| | 12-14 | 3.0 + 5.0 | Repaso | Snowpipe, descarga de datos, Data Sharing |
| **Semana 3** | 15-16 | 4.0 (21%) | Leer y practicar | Dynamic Tables, Streams, Tasks, clustering, ventanas |
| | 17-18 | 4.0 | Laboratorio DORA | **Insignia 5** (Data Engineering) |
| | 19-21 | 2.0 (20%) | Leer y practicar | Roles, RBAC, masking, resource monitors, network policies |
| **Semana 4** | 22-23 | 2.0 + 5.0 | Laboratorio DORA | **Insignia 2** (Collaboration, Marketplace & Cost) |
| | 24-25 | Repaso general | Releer los 3 archivos + tomar notas | Todos los archivos |
| | 26-27 | Examen de práctica | Simulacro de 100 preguntas en 115 min | Snowflake Practice Exam ($) o gratuitos |
| | 28-30 | Repaso de errores | Enfócate en preguntas fallidas del simulacro | Refuerza dominios débiles |

---

## Mapa de archivos

| Archivo | Contenido | Útil para |
|---|---|---|
| `informe_snowflake.md` | 30 preguntas tipo examen con respuestas y explicaciones | Dominios 1 y 3 principalmente |
| `plan_estudio_snowpro_core.md` | 21 temas extendidos NO cubiertos en las 30 preguntas | Dominios 2, 4 y 5 |
| `guia_dora_badges.md` | Mapeo de insignias DORA a temas del examen | Práctica hands-on de todos los dominios |
| **Este archivo** | Mapeo completo COF-C03 + plan de estudio | **Hoja de ruta general** |

---

## Checklist final pre-examen

- [ ] Conozco la arquitectura de 3 capas (Cloud Services, Compute, Storage)
- [ ] Sé la diferencia entre Time Travel y Fail-safe (días exactos)
- [ ] Puedo explicar zero-copy cloning
- [ ] Distingo tablas permanentes, transitorias y temporales
- [ ] Conozco los 4 tipos de stage y cómo usarlos
- [ ] Sé qué hace COPY INTO (carga y descarga)
- [ ] Puedo listar los roles del sistema y su jerarquía
- [ ] Entiendo Masking Policies y Row Access Policies
- [ ] Puedo crear un Resource Monitor
- [ ] Sé la diferencia entre Dynamic Table, Materialized View y View normal
- [ ] Entiendo cómo funcionan Tasks y Streams (CDC)
- [ ] Conozco los formatos semiestructurados que soporta Snowflake
- [ ] Sé qué hace FLATTEN y sus columnas (VALUE, KEY, INDEX)
- [ ] Entiendo Data Sharing, Reader Accounts y Marketplace
- [ ] Puedo configurar auto-suspend y auto-resume en un warehouse
- [ ] Sé cómo usar `LIMIT` sin `ORDER BY` (comportamiento no determinista)
- [ ] Conozco las ediciones y sus características
- [ ] He hecho al menos 2 laboratorios DORA completos

---

> **Nota final:** Las 30 preguntas del informe original son una muestra representativa pero NO exhaustiva. El examen real tiene 100 preguntas. El plan de estudio de 21 temas y los laboratorios DORA son esenciales para cubrir el 100% del temario. ¡Buena suerte!
