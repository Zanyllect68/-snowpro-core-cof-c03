# Plan Horario Detallado — SnowPro Core COF-C03

> Basado en 30 días, ~2 horas/día (60 horas totales).  
> Ajusta las horas según tu disponibilidad real.

---

## Distribución por dominio (horas totales)

| Dominio | % Examen | Horas sugeridas |
|---|---|---|
| 1. Arquitectura y características | 31% | 18.5 h |
| 2. Gestión de cuentas y gobernanza | 20% | 12 h |
| 3. Carga, descarga y conectividad | 18% | 11 h |
| 4. Optimización, consultas y transformación | 21% | 12.5 h |
| 5. Colaboración de datos | 10% | 6 h |
| **Total** | **100%** | **60 h** |

---

## Cronograma día por día

### SEMANA 1 — Dominio 1 (Arquitectura) — 18.5 h

| Día | Tema | Tiempo | Material | Práctica |
|---|---|---|---|---|
| 1 | Arquitectura multicapa (Cloud Services, Compute, Storage) | 1.5 h | `plan_estudio` Secc. 1 | Diagramar las 3 capas |
| 2 | Microparticiones y cómo funcionan | 1.5 h | `plan_estudio` Secc. 1 | Consultar `SYSTEM$CLUSTERING_DEPTH` |
| 3 | Partition pruning y clustering keys | 1.5 h | `plan_estudio` Secc. 1 | `CLUSTER BY`, `SYSTEM$CLUSTERING_INTERVAL` |
| 4 | Time Travel (AT, BEFORE, días) | 1.5 h | `informe` Preg 04, 16; `plan_estudio` Secc. 4 | `AT(TIMESTAMP =>)`, `BEFORE(STATEMENT =>)` |
| 5 | Fail-safe (7 fijo vs Time Travel configurable) | 1 h | `plan_estudio` Secc. 4 | Repasar diferencias |
| 6 | Zero-copy cloning | 1.5 h | `plan_estudio` Secc. 3 | `CREATE TABLE CLONE`, clonar BD |
| 7 | Tipos de tabla (permanente, transitoria, temporal) | 1 h | `plan_estudio` Secc. 5 | Crear cada tipo y ver duración |
| 8 | Almacenes virtuales (sizing, auto-suspend, auto-resume) | 1.5 h | `informe` Preg 05, 22 | Crear warehouses XS a XL, probar |
| 9 | Ediciones de Snowflake (Standard, Enterprise, BC, VPS) | 1 h | `plan_estudio` Secc. 8 | Tabla comparativa |
| 10 | Caching (result, metadata, local disk) | 1 h | `plan_estudio` Secc. 2 | `USE_CACHED_RESULT = FALSE` |
| 11 | Snowsight y hojas de trabajo | 0.5 h | `informe` Preg 03, 19 | Navegar Snowsight |
| 12 | Notebooks y Cortex AI | 1.5 h | `informe` Preg 06, 07, 09, 15, 18, 29 | Celda SQL + Python, `{{myvar}}` |
| 13 | Repaso General Dominio 1 | 1.5 h | Flashcards / resumen | Preguntas tipo |
| 14 | **Laboratorio DORA — Insignia 1** | 2 h | Data Warehousing Workshop | Completar badge |

---

### SEMANA 2 — Dominio 3 (Carga/Descarga) + Dominio 5 (Colaboración) — 17 h

| Día | Tema | Tiempo | Material | Práctica |
|---|---|---|---|---|
| 15 | Stages: user `@~`, table `@%`, named, interno vs externo | 1.5 h | `plan_estudio` Secc. 6 | `LIST @~`, `CREATE STAGE`, `DROP STAGE` |
| 16 | COPY INTO (carga de stage a tabla) | 1.5 h | `informe` Preg 02, 12, 17 | `COPY INTO table FROM @stage` |
| 17 | Formatos de archivo (CSV, JSON, Parquet, Avro, ORC) | 1.5 h | `informe` Preg 28 | `FILE_FORMAT = (TYPE = CSV)` |
| 18 | Datos semiestructurados (VARIANT, FLATTEN) | 1.5 h | `informe` Preg 24; `plan_estudio` Secc. 17 | `FLATTEN(INPUT => column)` |
| 19 | Datos no estructurados y PARSE_DOCUMENT | 1 h | `informe` Preg 20, 25 | Extraer texto de PDF en stage |
| 20 | Snowpipe (carga automatizada) | 1.5 h | Docs Snowflake + plan | `CREATE PIPE`, `ALTER PIPE REFRESH` |
| 21 | Descarga de datos (COPY INTO location) | 1 h | Docs Snowflake | `COPY INTO @stage FROM table` |
| 22 | Secure Data Sharing y Reader Accounts | 1.5 h | `plan_estudio` Secc. 20 | `CREATE SHARE`, `GRANT SELECT` |
| 23 | Marketplace, Data Exchange, Listings | 1 h | `informe` Preg 08 | Explorar Marketplace |
| 24 | Auto-fulfillment y Private Data Exchange | 0.5 h | `plan_estudio` Secc. 20 | Repaso conceptual |
| 25 | **Laboratorio DORA — Insignia 4 + 2** | 3 h | Data Lake + Collaboration | Completar ambos badges |

---

### SEMANA 3 — Dominio 4 (Optimización y Consultas) — 12.5 h

| Día | Tema | Tiempo | Material | Práctica |
|---|---|---|---|---|
| 26 | Sintaxis SQL avanzada (JOINs, CTEs, subconsultas) | 1.5 h | `informe` Preg 13, 30 | Practicar JOINs, WITH, subqueries |
| 27 | Funciones de ventana (RANK, DENSE_RANK, LAG, LEAD) | 1.5 h | `plan_estudio` Secc. 18 | `ROW_NUMBER() OVER (PARTITION BY ...)` |
| 28 | Dynamic Tables | 1.5 h | `plan_estudio` Secc. 9 | `CREATE DYNAMIC TABLE ... TARGET_LAG = '5 minutes'` |
| 29 | Materialized Views vs Views vs Dynamic Tables | 1 h | `plan_estudio` Secc. 9 | Crear los 3 tipos y comparar |
| 30 | Tasks y Streams (CDC) | 2 h | `plan_estudio` Secc. 10 | `CREATE STREAM`, `CREATE TASK`, tarea encadenada |
| 31 | EXPLAIN y Query Profile en Snowsight | 1.5 h | `plan_estudio` Secc. 19 | `EXPLAIN SELECT`, leer plan |
| 32 | Search Optimization Service | 0.5 h | `plan_estudio` Secc. 19 | `ALTER TABLE ADD SEARCH OPTIMIZATION` |
| 33 | Repaso Dominio 4 | 1.5 h | Flashcards / resumen | Preguntas tipo |
| 34 | **Laboratorio DORA — Insignia 5** | 2 h | Data Engineering Workshop | Completar badge |

---

### SEMANA 4 — Dominio 2 (Gobernanza) + Repaso General — 12 h

| Día | Tema | Tiempo | Material | Práctica |
|---|---|---|---|---|
| 35 | Roles del sistema y jerarquía (ACCOUNTADMIN → PUBLIC) | 1 h | `plan_estudio` Secc. 11; `informe` Preg 23 | `SHOW ROLES` |
| 36 | RBAC: crear roles, otorgar privilegios, herencia | 1.5 h | `plan_estudio` Secc. 11 | `CREATE ROLE`, `GRANT ROLE TO ROLE` |
| 37 | Masking Policies | 1.5 h | `plan_estudio` Secc. 12 | `CREATE MASKING POLICY`, `ALTER TABLE ... SET MASKING POLICY` |
| 38 | Row Access Policies | 1 h | `plan_estudio` Secc. 12 | `CREATE ROW ACCESS POLICY` |
| 39 | Network Policies | 0.5 h | `plan_estudio` Secc. 12 | `CREATE NETWORK POLICY` |
| 40 | Resource Monitors (credit quota, triggers, acciones) | 1.5 h | `plan_estudio` Secc. 7 | `CREATE RESOURCE MONITOR`, probar NOTIFY, SUSPEND |
| 41 | Conectividad: MFA, SSO, OAuth, Key Pair, Private Link | 1 h | `plan_estudio` Secc. 15 | Repaso conceptual |
| 42 | **Examen de práctica #1** | 2 h (115 min) | Simulacro 100 preg | Sin material, cronometrado |
| 43 | Revisar errores del simulacro | 1.5 h | Identificar dominios débiles | Repasar solo temas fallidos |
| 44 | Repasar dominios 2 y 4 (basado en errores) | 1.5 h | Según resultados | Flashcards + preguntas |
| 45 | **Examen de práctica #2** (si hay tiempo) | 2 h | Segundo simulacro | Meta: 800+ |
| 46 | **Repaso final** — Leer los 3 archivos completos | 1.5 h | `informe` + `plan_estudio` + `guia_completa` | Checklist pre-examen |

---

## Resumen semanal

| Semana | Horas | Dominios | Badge DORA |
|---|---|---|---|
| 1 | 18.5 h | 1.0 Arquitectura (31%) | Insignia 1 |
| 2 | 17 h | 3.0 Carga (18%) + 5.0 Colaboración (10%) | Insignia 4 + 2 |
| 3 | 12.5 h | 4.0 Optimización (21%) | Insignia 5 |
| 4 | 12 h | 2.0 Gobernanza (20%) + Repasos + Simulacros | — |

---

## Ritmo sugerido según disponibilidad

| Disponibilidad | Horas/día | Días totales | Calendario |
|---|---|---|---|
| **Intensivo** | 4 h/día | 15 días | 2 semanas |
| **Medio** | 2 h/día | 30 días | 1 mes |
| **Relajado** | 1 h/día | 60 días | 2 meses |
| **Express** | 6 h/día | 10 días | Solo si ya tienes experiencia |

---

> **Pro tip:** Los laboratorios DORA (Insignias) son la mejor inversión de tiempo. Cada badge te da práctica real con los comandos exactos que preguntan en el examen. No los saltes.
