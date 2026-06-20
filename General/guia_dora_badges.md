# Guía de Estudio SnowPro Core — Ruta DORA Badges (Hands-on)

> **¿Qué es DORA?** Es un sistema automatizado de calificación dentro de los talleres de Snowflake. Completas laboratorios prácticos y envías pruebas; DORA verifica tu trabajo y te otorga insignias (*badges*) para compartir en LinkedIn. Todo es gratuito.

---

## Organización por temas del examen

Cada tema incluye: qué insignia(s) DORA lo practican, dónde estudiarlo en los apuntes, y sintaxis clave.

---

### DOMINIO 1 — Arquitectura y Características (31%)

#### 1.1 Arquitectura multicapa (Cloud Services, Compute, Storage)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.1 | `plan_estudio_snowpro_core.md` — Secc. 1 | `../01_Arquitectura/Snowflake Functional Architecture.md` |
| **Práctica** | Diagramar las 3 capas. Crear warehouse, BD y esquemas. Separar carga de trabajo por equipo. |

#### 1.2 Microparticiones y Clustering

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing), Insignia 5 (Data Engineering) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.2 | `plan_estudio_snowpro_core.md` — Secc. 1 | `../01_Arquitectura/Micro-Partitions and Data Clustering.md` |
| **Sintaxis clave** | `ALTER TABLE t CLUSTER BY (col)` | `SYSTEM$CLUSTERING_DEPTH('t')` | `SYSTEM$CLUSTERING_INTERVAL('t', 'col')` |
| **Práctica** | Verificar profundidad de clúster, probar partition pruning con filtros por fecha. |

#### 1.3 Time Travel

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.3 | `plan_estudio_snowpro_core.md` — Secc. 4 | `Data Protection and Sharing.md` | `informe_snowflake.md` — Preg 04, 16 |
| **Sintaxis clave** | `SELECT * FROM t AT(TIMESTAMP => '...')` | `SELECT * FROM t BEFORE(STATEMENT => '...')` | `AT(OFFSET => -300)` | `ALTER TABLE t SET DATA_RETENTION_TIME_IN_DAYS = N` |
| **Práctica** | Default: 1 día. Máx: 90d (Enterprise). Configurar a nivel tabla/esquema/BD/cuenta. |

#### 1.4 Fail-safe

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.4 | `plan_estudio_snowpro_core.md` — Secc. 4 | `../02_Gobernanza/Data Protection and Business Continuity.md` |
| **Clave** | 7 días fijos NO configurables. Solo Snowflake accede. Después de Time Travel. No aplica a tablas transitorias/temporales. |

#### 1.5 Zero-copy Cloning

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.5 | `plan_estudio_snowpro_core.md` — Secc. 3 | `Data Protection and Sharing.md` |
| **Sintaxis clave** | `CREATE TABLE t2 CLONE t1` | `CREATE SCHEMA s2 CLONE s1` | `CREATE DATABASE d2 CLONE d1` | `CREATE TABLE t3 CLONE t1 AT(TIMESTAMP => '...')` |
| **Práctica** | Clonar tabla, modificar datos en el clon, verificar que el original no cambia. |

#### 1.6 Tipos de Tabla

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.6 | `plan_estudio_snowpro_core.md` — Secc. 5 | `../01_Arquitectura/Tables Types and Views.md` |
| **Sintaxis clave** | `CREATE TRANSIENT TABLE t (id INT)` | `CREATE TEMPORARY TABLE t (id INT)` |
| **Práctica** | Permanente (TT 1-90d + Fail-safe) vs Transitoria (TT 1d, sin Fail-safe) vs Temporal (solo sesión, sin Fail-safe). |

#### 1.7 Almacenes Virtuales (Warehouses)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing), Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.7 | `../01_Arquitectura/Virtual_Warehouses_types,_Sizing_and_Scaling.md` | `informe_snowflake.md` — Preg 05, 22 |
| **Sintaxis clave** | `CREATE WAREHOUSE w WITH WAREHOUSE_SIZE='XSMALL' AUTO_SUSPEND=5 AUTO_RESUME=TRUE` |
| **Práctica** | Probar sizing (XS a 6XL), auto-suspend, auto-resume, multi-cluster (Enterprise+). Escalamiento vertical (más grande) vs horizontal (más clústeres). |

#### 1.8 Ediciones de Snowflake

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.8 | `plan_estudio_snowpro_core.md` — Secc. 8 | `../01_Arquitectura/Snowflake Functional Architecture.md` |
| **Clave** | Standard (TT 1d) → Enterprise (TT 90d, multi-cluster, mat views) → Business Critical (HIPAA, column-level security) → VPS (aislado, Private Link). |

#### 1.9 Caching

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.9 | `plan_estudio_snowpro_core.md` — Secc. 2 |
| **Clave** | Result Cache (24h, no necesita warehouse), Metadata Cache (siempre disponible), Local Disk SSD (mientras warehouse activo). |

#### 1.10 Snowsight e Interfaces

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.10 | `Ways of Working with Snowflake.md` | `informe_snowflake.md` — Preg 03, 19, 26 |
| **Clave** | Database Explorer, Data Preview (100 filas), Query History, Worksheets/Workspaces. VS Code Extension y Snowflake CLI como alternativas. |

#### 1.11 Notebooks y Cortex AI

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 6 (Data Science Workshop) |
| **Apuntes** | `apuntes_snowpro_core.md` — 1.11 | `Snowflake Cortex and Ml Features.md` | `informe_snowflake.md` — Preg 06, 07, 09, 15, 18, 29 |
| **Sintaxis clave** | `SELECT COMPLETE('model', 'prompt')` | `{{myvar}}` en SQL desde Python | Celda verde = ejecutada sin errores |
| **Práctica** | Crear notebook con celdas SQL+Python, probar `COMPLETE()`, `CLASSIFY_TEXT()`, `TRANSLATE()`, `PARSE_DOCUMENT()`. |

---

### DOMINIO 2 — Gestión de Cuentas y Gobernanza (20%)

#### 2.1 Roles del Sistema

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.1 | `plan_estudio_snowpro_core.md` — Secc. 11 | `../02_Gobernanza/RBAC, DAC, and the Securable Object Hierarchy.md` | `informe_snowflake.md` — Preg 23 |
| **Jerarquía** | `ORGADMIN` → `ACCOUNTADMIN` → `SYSADMIN` (horizontal) y `SECURITYADMIN` → `USERADMIN` (vertical). `PUBLIC` es base para todos. |

#### 2.2 RBAC y Privilegios

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing), Insignia 3 (Data Applications) |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.2 | `plan_estudio_snowpro_core.md` — Secc. 11, 16 | `../02_Gobernanza/Custom Roles and Secondary Roles.md` | `Creating And Managing Database Objects.md` | `informe_snowflake.md` — Preg 21 |
| **Sintaxis clave** | `CREATE ROLE analyst` | `GRANT USAGE ON DATABASE db TO ROLE analyst` | `GRANT SELECT ON ALL TABLES IN SCHEMA db.sch TO ROLE analyst` | `GRANT ROLE analyst TO USER u` |
| **Práctica** | Crear roles de acceso y roles funcionales, jerarquía, roles secundarios (`SET SECONDARY ROLES ALL`), subvenciones futuras (`GRANT SELECT ON FUTURE TABLES`). |

#### 2.3 Masking Policies

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.3 | `plan_estudio_snowpro_core.md` — Secc. 12 | `../02_Gobernanza/Column -level and Row-Level Security.md` |
| **Sintaxis clave** | `CREATE MASKING POLICY p AS (val STRING) RETURNS STRING -> CASE WHEN CURRENT_ROLE() IN ('ADMIN') THEN val ELSE '***' END` | `ALTER TABLE t MODIFY COLUMN c SET MASKING POLICY p` |
| **Práctica** | Usar `IS_ROLE_IN_SESSION()` vs `CURRENT_ROLE()` para roles secundarios. Tokenización externa como alternativa. |

#### 2.4 Row Access Policies

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.4 | `plan_estudio_snowpro_core.md` — Secc. 12 | `../02_Gobernanza/Column -level and Row-Level Security.md` |
| **Sintaxis clave** | `CREATE ROW ACCESS POLICY r AS (region STRING) RETURNS BOOLEAN -> CURRENT_ROLE() IN ('ADMIN') OR region = 'PUBLIC'` | `ALTER TABLE t ADD ROW ACCESS POLICY r ON (region)` |
| **Práctica** | Row policy se aplica antes que masking. Combinar ambas en misma tabla. |

#### 2.5 Network Policies

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.5 | `plan_estudio_snowpro_core.md` — Secc. 12 | `../02_Gobernanza/Authentication Methods and Network Policies.md` |
| **Sintaxis clave** | `CREATE NETWORK RULE r ALLOWED_IP_LIST=('192.168.1.0/24')` | `CREATE NETWORK POLICY p ALLOWED_NETWORK_RULE_LIST=(r)` | `ALTER ACCOUNT SET NETWORK POLICY = p` |

#### 2.6 Resource Monitors

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.6 | `plan_estudio_snowpro_core.md` — Secc. 7 | `../02_Gobernanza/Resource Monitors and Credit Calculation.md` |
| **Sintaxis clave** | `CREATE RESOURCE MONITOR m WITH CREDIT_QUOTA=5000 FREQUENCY=MONTHLY TRIGGERS ON 80% DO NOTIFY ON 100% DO SUSPEND ON 110% DO SUSPEND_IMMEDIATE` | `ALTER WAREHOUSE w SET RESOURCE_MONITOR = m` |
| **Práctica** | Nivel cuenta vs warehouse. Acciones: NOTIFY, SUSPEND, SUSPEND_IMMEDIATE. Frecuencias: MONTHLY, DAILY, WEEKLY, YEARLY, NEVER. |

#### 2.7 Conectividad y Seguridad

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 3 (Data Applications) |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.7 | `plan_estudio_snowpro_core.md` — Secc. 15 | `../02_Gobernanza/Authentication Methods and Network Policies.md` |
| **Clave** | MFA (Passkey, TOTP), SSO (SAML con Okta/Entra ID), OAuth, Key Pair Auth (RSA), Private Link (AWS/Azure/GCP sin internet). |

#### 2.8 Object Tagging y Data Classification

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.10 | `../02_Gobernanza/Object Tagging Data Classification, and Privacy Policies.md` |
| **Sintaxis clave** | `CREATE TAG sensitivity ALLOWED_VALUES 'PII', 'CONFIDENTIAL', 'INTERNAL'` | `ALTER TABLE t MODIFY COLUMN c SET TAG sensitivity = 'PII'` |
| **Práctica** | Tags heredan (esquema → tabla → columna). Clasificación automática con Cortex. Privacy Policies vinculan clasificación con masking. |

#### 2.9 Data Lineage y Trust Center

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `../02_Gobernanza/Data Lineae and Trust Center.md` |
| **Clave** | Linaje: objetos upstream (fuentes) y downstream (dependencias). Access History en `ACCOUNT_USAGE.ACCESS_HISTORY`. Trust Center: CIS Benchmark, Security Essentials, Threat Intelligence. |

#### 2.10 Encryption, Alerts y Notifications

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `../02_Gobernanza/Encryption, Alerts, and Notifications.md` |
| **Clave** | AES-256 en reposo, TLS 1.2+ en tránsito. Claves administradas por Snowflake o cliente (AWS KMS, Azure Key Vault, GCP KMS). Tri-Secret Secure (BC+). Alertas: `CREATE ALERT` con condición SQL + acción `SYSTEM$SEND_SNOWFLAKE_NOTIFICATION`. |

#### 2.11 Replicación y Failover

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 2.8 | `plan_estudio_snowpro_core.md` — Secc. 13 | `../02_Gobernanza/Data Protection and Business Continuity.md` |
| **Sintaxis clave** | `ALTER DATABASE db ENABLE REPLICATION TO ACCOUNTS org.acct` | Replication Groups (solo datos) vs Failover Groups (datos + objetos de cuenta). |

#### 2.12 Monitoring con ACCOUNT_USAGE

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `../02_Gobernanza/Monitoring with ACCOUNT_USAGE.md` |
| **Vistas clave** | `WAREHOUSE_METERING_HISTORY` (créditos por almacén), `QUERY_HISTORY` (consultas lentas), `STORAGE_USAGE` (almacenamiento), `LOGIN_HISTORY` (intentos de conexión). Latencia: hasta 3h. Retención: 365 días. |

---

### DOMINIO 3 — Carga y Descarga de Datos (18%)

#### 3.1 Stages

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing), Insignia 4 (Data Lake) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.1 | `plan_estudio_snowpro_core.md` — Secc. 6 | `../03_Carga_Descarga/Loading Structured and Same-Structured Data.md` | `informe_snowflake.md` — Preg 20 |
| **Sintaxis clave** | `LIST @~` | `LIST @%table_name` | `CREATE STAGE s` | `CREATE STAGE s URL='s3://bucket/' CREDENTIALS=(...)` | `REMOVE @s` |
| **Práctica** | User (`@~`), Table (`@%table`), Named interno, Named externo (S3/GCS/Azure). |

#### 3.2 COPY INTO (Carga)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing), Insignia 5 (Data Engineering) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.2 | `../03_Carga_Descarga/Loading Structured and Same-Structured Data.md` | `informe_snowflake.md` — Preg 02, 12, 17 |
| **Sintaxis clave** | `COPY INTO t FROM @s FILE_FORMAT=(TYPE=CSV SKIP_HEADER=1)` |
| **Práctica** | Requiere 3 objetos: stage, tabla y warehouse. Carga bulk, no INSERT. |

#### 3.3 Formatos de Archivo

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 4 (Data Lake) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.3 | `informe_snowflake.md` — Preg 28 |
| **Sintaxis clave** | `CREATE FILE FORMAT f TYPE=JSON` | `CREATE FILE FORMAT f TYPE=CSV SKIP_HEADER=1` |
| **Clave** | Soportados: CSV, JSON, Avro, Parquet, ORC, XML. Semiestructurados nativos: JSON, Avro, ORC, Parquet. NO nativos: YAML, HTML, VCF. |

#### 3.4 Datos Semiestructurados (VARIANT, FLATTEN)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 4 (Data Lake) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.4 | `plan_estudio_snowpro_core.md` — Secc. 17 | `informe_snowflake.md` — Preg 24 |
| **Sintaxis clave** | `SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('{"a":1}')))` | Columna `VALUE`, también `KEY`, `INDEX`, `SEQ`, `PATH` |
| **Práctica** | VARIANT guarda JSON sin esquema predefinido. Notación `:` para navegar, `::` para castear. |

#### 3.5 Datos No Estructurados (PARSE_DOCUMENT)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 4 (Data Lake) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.5 | `../03_Carga_Descarga/Working with Unstructured Data.md` | `informe_snowflake.md` — Preg 25 |
| **Sintaxis clave** | `SELECT PARSE_DOCUMENT('@stage/doc.pdf', 'PDF')::STRING` | Directorio: `ALTER STAGE s SET DIRECTORY = (ENABLE = TRUE)` |
| **Práctica** | Archivos en stages (no en tablas). Tablas de directorio catalogan archivos. URLs pre-firmadas (`GET_PRESIGNED_URL`) para acceso externo. |

#### 3.6 Snowpipe

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.6 |
| **Sintaxis clave** | `CREATE PIPE p AS COPY INTO t FROM @s FILE_FORMAT=(TYPE=JSON)` | `ALTER PIPE p REFRESH` |
| **Práctica** | Carga automatizada continua basada en eventos (SQS/SNS, GCS Pub/Sub, Azure Events). |

#### 3.7 Descarga de Datos (COPY INTO location)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.7 |
| **Sintaxis clave** | `COPY INTO @s/data/ FROM t FILE_FORMAT=(TYPE=PARQUET)` |

#### 3.8 External Tables e Iceberg Tables

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 4 (Data Lake) |
| **Apuntes** | `apuntes_snowpro_core.md` — 3.8 | `plan_estudio_snowpro_core.md` — Secc. 14 |
| **Sintaxis clave** | `CREATE EXTERNAL TABLE t LOCATION=@ext_stage FILE_FORMAT=(TYPE=PARQUET)` |
| **Clave** | External Table (solo lectura, datos en S3/GCS/Azure). Iceberg Table (Apache Iceberg, lectura/escritura, catálogo Snowflake o externo). |

---

### DOMINIO 4 — Optimización y Transformación (21%)

#### 4.1 SQL Avanzado

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 1 (Data Warehousing) |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.1 | `informe_snowflake.md` — Preg 13, 30 |
| **Clave** | `SELECT *` = todas las columnas. `LIMIT` sin `ORDER BY` = no determinista. CTEs con `WITH`. JOINs (INNER, LEFT, RIGHT, FULL). |

#### 4.2 Funciones de Ventana

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 6 (Data Science Workshop) |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.2 | `plan_estudio_snowpro_core.md` — Secc. 18 |
| **Sintaxis clave** | `ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC)` | `RANK()` | `DENSE_RANK()` | `LAG()` | `LEAD()` | `SUM() OVER (PARTITION BY ... ORDER BY ...)` |

#### 4.3 Dynamic Tables

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 5 (Data Engineering) |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.3 | `plan_estudio_snowpro_core.md` — Secc. 9 |
| **Sintaxis clave** | `CREATE DYNAMIC TABLE dt TARGET_LAG='5 minutes' WAREHOUSE=w AS SELECT ...` |
| **Práctica** | Refresco automático. Almacenan datos. Alternativa a Tasks+Streams para ETL. |

#### 4.4 Materialized Views

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 5 (Data Engineering) |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.4 | `plan_estudio_snowpro_core.md` — Secc. 9 | `../01_Arquitectura/Tables Types and Views.md` |
| **Sintaxis clave** | `CREATE MATERIALIZED VIEW mv AS SELECT category, COUNT(*) FROM products GROUP BY category` |
| **Comparativa** | View (no almacena, gratis) vs Materialized View (almacena, auto-refresh con costo) vs Dynamic Table (target lag configurable, almacena). |

#### 4.5 Tasks y Streams (CDC)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 5 (Data Engineering), Insignia 3 (Data Applications) |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.5 | `plan_estudio_snowpro_core.md` — Secc. 10 |
| **Sintaxis clave** | `CREATE TASK t WAREHOUSE=w SCHEDULE='5 MINUTE' AS INSERT INTO log SELECT * FROM stream` | `CREATE TASK t2 AFTER t AS DELETE FROM temp` | `CREATE STREAM s ON TABLE t` |
| **Práctica** | Tasks programadas o encadenadas (AFTER). Streams capturan INSERT/UPDATE/DELETE. Offset avanza al consumir. Pipeline incremental: Task + Stream. |

#### 4.6 EXPLAIN y Query Profile

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.6 | `plan_estudio_snowpro_core.md` — Secc. 19 |
| **Sintaxis clave** | `EXPLAIN SELECT ...` | `USE_CACHED_RESULT = FALSE` para pruebas sin caché |
| **Práctica** | EXPLAIN: plan textual. Query Profile en Snowsight: identificar cuellos de botella (tablescans, joins costosos). |

#### 4.7 Search Optimization Service

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 4.7 | `plan_estudio_snowpro_core.md` — Secc. 19 |
| **Sintaxis clave** | `ALTER TABLE t ADD SEARCH OPTIMIZATION ON (col)` |
| **Clave** | Mejora búsquedas por punto y subcadenas. Costo adicional de almacenamiento. Útil en tablas grandes. |

---

### DOMINIO 5 — Colaboración de Datos (10%)

#### 5.1 Secure Data Sharing

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 5.1 | `plan_estudio_snowpro_core.md` — Secc. 20 | `Data Protection and Sharing.md` |
| **Sintaxis clave** | `CREATE SHARE s` | `GRANT USAGE ON DATABASE db TO SHARE s` | `GRANT SELECT ON TABLE db.sch.t TO SHARE s` | `ALTER SHARE s ADD ACCOUNTS = org.acct` |
| **Clave** | Sin copia de datos. Consumidor ve datos frescos. Cuentas PRO solo consumidoras de cuentas Standard. |

#### 5.2 Reader Accounts

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 5.2 | `plan_estudio_snowpro_core.md` — Secc. 20 |
| **Clave** | Compartir con cuentas que NO son Snowflake. Solo lectura. Para clientes/partners externos. |

#### 5.3 Marketplace vs Data Exchange

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 2 (Collaboration, Marketplace & Cost) |
| **Apuntes** | `apuntes_snowpro_core.md` — 5.3 | `informe_snowflake.md` — Preg 08 |
| **Clave** | Marketplace (público, cualquier cuenta). Data Exchange (privado, dentro de organización). Mismo rendimiento (ambos usan Secure Data Sharing). |

#### 5.4 Auto-fulfillment

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `apuntes_snowpro_core.md` — 5.4 | `plan_estudio_snowpro_core.md` — Secc. 20 |
| **Clave** | Mecanismo de respaldo si el provider está en región diferente. Transparente para el consumidor. |

---

### HERRAMIENTAS ADICIONALES

#### Snowflake CoCo (AI Agent)

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 6 (Data Science Workshop) |
| **Apuntes** | `Snowflake CoCo.md` |
| **Clave** | Agente AI integrado en Snowsight. Escribe/repara SQL, explora datos en lenguaje natural, crea proyectos dbt, habilidades integradas con `/`. |

#### Snowpark

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | Insignia 3 (Data Applications) |
| **Apuntes** | `Tools for Every Team.md` |
| **Clave** | Biblioteca Python/Scala/Java para ejecutar código dentro de Snowflake. ETL, ML batch, UDFs. El código va a los datos. |

#### Streamlit en Snowflake

| Aspecto | Detalle |
|---|---|
| **Insignia DORA** | No cubierto directamente en badges estándar |
| **Apuntes** | `Tools for Every Team.md` |
| **Clave** | Apps interactivas en Python dentro de Snowflake. Datos no salen de la plataforma. |

---

## Ruta recomendada en orden

```
  Insignia 1 (Data Warehousing)
       ↓
  Insignia 2 (Collaboration, Marketplace & Cost)
       ↓
  [Elige 1 de las 4]:
     ├─ Insignia 3 (Data Applications)
     ├─ Insignia 4 (Data Lake)
     ├─ Insignia 5 (Data Engineering)  ← Recomendada para SnowPro Core
     └─ Insignia 6 (Data Science)
```

**Si tu objetivo es solo el SnowPro Core**, prioriza:
1. **Insignia 1** — Cubre ~40% del examen (arquitectura, warehouses, tablas, cloning, time travel)
2. **Insignia 2** — Cubre ~15% del examen (data sharing, resource monitors, costos)
3. **Insignia 5** — Cubre ~25% del examen (dynamic tables, streams, tasks, clustering)

---

## Cómo estudiar con este material

| Paso | Qué hacer |
|---|---|
| 1 | Elige un tema de esta guía (ej. "Time Travel") |
| 2 | Lee la sección en `apuntes_snowpro_core.md` |
| 3 | Revisa los archivos específicos listados como "Apuntes" |
| 4 | Abre el taller DORA indicado en "Insignia DORA" |
| 5 | Practica la sintaxis clave del tema |
| 6 | Repite hasta dominar el tema antes de pasar al siguiente |

---

## ¿Dónde acceder a los talleres DORA?

1. Ve a https://learn.snowflake.com/
2. Busca **"Hands-On Essentials"**
3. Elige cualquiera de los laboratorios (todos gratuitos)
4. Creas una cuenta trial Snowflake (gratis, sin tarjeta)
5. Sigues el laboratorio paso a paso
6. Ejecutas el código DORA al final para validar y obtener tu insignia

---

> **Consejo clave:** Las insignias DORA te dan **experiencia práctica** que el examen SnowPro Core evalúa. Esta guía te permite estudiar por tema y saber exactamente qué badge practica cada concepto y dónde están los apuntes teóricos para complementar.
