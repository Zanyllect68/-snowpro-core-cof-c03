# Apuntes SnowPro Core — COF-C03

> Organizado por los 5 dominios oficiales del examen.  
> Contenido fusionado de: `informe_snowflake.md`, `plan_estudio_snowpro_core.md`, `guia_completa_COF-C03.md`, `guia_dora_badges.md`

---

## Datos del Examen

| Aspecto | Valor |
|---|---|
| Preguntas | 100 |
| Tiempo | 115 min |
| Aprobación | 750/1000 |
| Costo | $175 USD |
| Versión | COF-C03 |

---

## Dominio 1 — Características y Arquitectura de Snowflake AI Data Cloud (31%)

### 1.1 Arquitectura multicapa

| Capa | Función | Componentes |
|---|---|---|
| **Cloud Services** | Autenticación, metadatos, optimización | Authentication, Metadata, Query Optimizer, Security |
| **Compute** | Procesamiento de consultas | Virtual Warehouses (XS a 6XL) |
| **Storage** | Almacenamiento de datos | Microparticiones en S3/GCS/Azure (comprimidas, columnar) |

- Cada capa se escala independientemente. No compiten por recursos.
- **Cloud Services** siempre está activo (no necesita warehouse).

### 1.2 Microparticiones y Clustering

| Concepto | Detalle |
|---|---|
| **Micropartición** | Unidad inmutable de ~50-500 MB comprimidos, formato columnar |
| **Metadatos** | Cada micropartición almacena min/max, null count, distinct values |
| **Partition Pruning** | Snowflake elimina automáticamente microparticiones irrelevantes usando metadatos |
| **Clustering Key** | Opcional. Útil en tablas >1TB con filtros por columnas específicas |
| **Auto-clustering** | Servicio gestionado que reordena microparticiones (costo adicional) |
| **Profundidad de clúster** | Métrica que indica cuántas microparticiones paralelas se deben escanear |

```sql
ALTER TABLE orders CLUSTER BY (customer_id, order_date);
SELECT SYSTEM$CLUSTERING_DEPTH('orders');
SELECT SYSTEM$CLUSTERING_INTERVAL('orders', 'order_date');
```

### 1.3 Time Travel

| Aspecto | Detalle |
|---|---|
| **Default** | 1 día (24 horas) |
| **Máximo** | 90 días (Enterprise en adelante) |
| **Parámetro** | `DATA_RETENTION_TIME_IN_DAYS` (0-90) |
| **Sintaxis** | `AT(TIMESTAMP =>)`, `BEFORE(STATEMENT =>)`, `OFFSET =>` |

```sql
SELECT * FROM table AT(TIMESTAMP => '2026-07-01 10:00:00');
SELECT * FROM table BEFORE(STATEMENT => '019a8b...');
SELECT * FROM table AT(OFFSET => -60*5);  -- 5 minutos atrás
ALTER TABLE table SET DATA_RETENTION_TIME_IN_DAYS = 3;
```

### 1.4 Fail-safe

| Aspecto | Detalle |
|---|---|
| **Duración** | 7 días fijos (NO configurables) |
| **Acceso** | Solo el equipo de Snowflake |
| **Costo** | Incluido en almacenamiento |
| **Propósito** | Recuperación de desastres |

**Línea de tiempo:**
```
Tabla activa → Time Travel (1-90 días configurable) → Fail-safe (7 días fijo) → Eliminación permanente
```

**Diferencia clave:** Time Travel es accesible por el usuario. Fail-safe solo por Snowflake.

### 1.5 Zero-copy Cloning

```sql
CREATE TABLE t2 CLONE t1;
CREATE SCHEMA s2 CLONE s1;
CREATE DATABASE d2 CLONE d1;
CREATE TABLE t3 CLONE t1 AT(TIMESTAMP => '2026-07-01');
```

- No copia datos físicamente, solo metadatos.
- Instantáneo, sin costo de almacenamiento adicional.
- Al modificar datos en el clon, se crean nuevas microparticiones (costo incremental).
- Funciona con tablas, esquemas y bases de datos completas.

### 1.6 Tipos de tabla

| Tipo | Duración | Persiste | Time Travel máximo |
|---|---|---|---|
| **Permanente** | Indefinida | Sí | 1-90 días |
| **Transitoria** | Indefinida | Sí | 1 día |
| **Temporal** | Solo la sesión | No | 1 día |

```sql
CREATE TRANSIENT TABLE t (id INT);
CREATE TEMPORARY TABLE t (id INT);
```

### 1.7 Almacenes Virtuales (Warehouses)

| Parámetro | Descripción |
|---|---|
| `WAREHOUSE_SIZE` | X-Small a 6X-Large |
| `AUTO_SUSPEND` | Minutos de inactividad antes de suspender (reduce costos) |
| `AUTO_RESUME` | Reanuda automáticamente al recibir consulta |
| `MULTI_CLUSTER` | Escalamiento horizontal (Enterprise+) |
| `MAX_CLUSTER_COUNT` | Número máximo de clústeres |

```sql
CREATE WAREHOUSE my_wh
  WITH WAREHOUSE_SIZE = 'XSMALL'
  AUTO_SUSPEND = 5
  AUTO_RESUME = TRUE;
```

- El dimensionamiento del warehouse se configura en el nivel de **Procesamiento de la Consulta**.
- Auto-suspend apaga el warehouse tras inactividad, reduciendo costos.

### 1.8 Ediciones de Snowflake

| Edición | Características clave |
|---|---|
| **Standard** | Time Travel 1d, Fail-safe 7d, compartición básica |
| **Enterprise** | Time Travel 90d, multi-cluster warehouses, materialized views |
| **Business Critical** | Todo Enterprise + HIPAA, HITRUST, column-level security |
| **VPS** | Todo BC + aislado con IP dedicada, Private Link, SOC2 Type 2 |

### 1.9 Caching

| Tipo de Cache | Alcance | Duración |
|---|---|---|
| **Result Cache** | Consultas repetidas | 24h (o hasta que cambien datos) |
| **Metadata Cache** | Cloud Services | Siempre disponible (sin warehouse) |
| **Local Disk Cache (SSD)** | Nodos del warehouse | Mientras el warehouse esté activo |

- El **Result Cache** NO requiere un warehouse funcionando.

### 1.10 Snowsight (Interfaz Web)

| Característica | Descripción |
|---|---|
| **Database Explorer** | Vista jerárquica de BD, esquemas y objetos |
| **Data Preview** | Muestra las primeras **100 filas** de una tabla |
| **Table Definition** | Visible en la pestaña Table Details |
| **Query History** | Historial de consultas ejecutadas |
| **Acciones en BD** | Renombrar (Edit) y Eliminar (Drop) desde el explorador |

- La interfaz web predeterminada es **Snowsight**.
- Las hojas de trabajo (worksheets) soportan SQL y Python.

### 1.11 Notebooks y Cortex AI

| Elemento | Detalle |
|---|---|
| **Notebooks** | Celdas SQL + Python + otros lenguajes |
| **Variables Python en SQL** | `{{myvar}}` |
| **Celda verde** | Ejecutada sin errores en la sesión actual |
| **Celda roja** | Error en la ejecución |
| **Botón Iniciar** | Activa la sesión del notebook (runtime) |
| **COMPLETE()** | Genera texto automáticamente usando LLM |
| **Cortex AI** | Extrae texto de datos no estructurados |

### 1.12 Esquemas

- Un **esquema** está contenido en una **base de datos**.
- Los esquemas se usan para **organizar objetos** de base de datos.
- Son mutables (se pueden modificar, clonar, eliminar).
- No contienen almacenes virtuales.

### 1.13 Objetos de Snowflake

| Objeto | Propósito |
|---|---|
| **Tabla** | Almacenar datos estructurados |
| **Vista** | Consulta almacenada (no almacena datos) |
| **Procedimiento** | Código almacenado (JavaScript, Python, SQL) |
| **Almacén virtual** | Procesamiento/cómputo |
| **Stage** | Almacenamiento de archivos (interno/externo) |

---

## Dominio 2 — Gestión de Cuentas y Gobernanza de Datos (20%)

### 2.1 Roles del Sistema

| Rol | Responsabilidad |
|---|---|
| `ORGADMIN` | Gestión a nivel de organización (crear cuentas) |
| `ACCOUNTADMIN` | Administración completa de la cuenta |
| `SECURITYADMIN` | Gestión de roles y usuarios |
| `USERADMIN` | Creación de usuarios y roles |
| `SYSADMIN` | Creación de objetos (warehouses, databases) |
| `PUBLIC` | Rol base que todos los usuarios tienen |

**Herencia:**
```
ACCOUNTADMIN
├── SYSADMIN (horizontal)
└── SECURITYADMIN
    └── USERADMIN (vertical)
```

### 2.2 RBAC y Privilegios

- **Forma recomendada:** Otorgar privilegios al rol (`GRANT privilege ON object TO ROLE`).
- `OWNERSHIP`: solo un rol puede tener ownership de un objeto.
- Roles secundarios: `SET SECONDARY ROLES ALL`.

```sql
CREATE ROLE analyst;
GRANT USAGE ON DATABASE db TO ROLE analyst;
GRANT SELECT ON ALL TABLES IN SCHEMA db.schema TO ROLE analyst;
GRANT ROLE analyst TO USER usuario1;
```

### 2.3 Masking Policies

Enmascara columnas según el rol del usuario que consulta.

```sql
CREATE MASKING POLICY email_mask AS (val STRING) RETURNS STRING ->
  CASE WHEN CURRENT_ROLE() IN ('ADMIN') THEN val ELSE '***' END;

ALTER TABLE users MODIFY COLUMN email SET MASKING POLICY email_mask;
```

### 2.4 Row Access Policies

Filtra filas completas según el rol.

```sql
CREATE ROW ACCESS POLICY region_filter AS (region STRING) RETURNS BOOLEAN ->
  CURRENT_ROLE() IN ('ADMIN','GLOBAL') OR region = 'PUBLIC';

ALTER TABLE sales ADD ROW ACCESS POLICY region_filter ON (region);
```

### 2.5 Network Policies

Restringe IPs que pueden conectarse a la cuenta.

```sql
CREATE NETWORK POLICY office_only
  ALLOWED_IP_LIST = ('192.168.1.0/24', '10.0.0.0/8')
  BLOCKED_IP_LIST = ('0.0.0.0/0');

ALTER ACCOUNT SET NETWORK POLICY = office_only;
```

### 2.6 Resource Monitors

Controlan el consumo de créditos. Acciones: NOTIFY, SUSPEND, SUSPEND_IMMEDIATE.

```sql
CREATE RESOURCE MONITOR monthly_limit
  WITH CREDIT_QUOTA = 5000
  FREQUENCY = MONTHLY
  START_TIMESTAMP = '2026-07-01 00:00'
  TRIGGERS ON 80% DO NOTIFY
           ON 100% DO SUSPEND
           ON 110% DO SUSPEND_IMMEDIATE;

ALTER WAREHOUSE my_wh SET RESOURCE_MONITOR = monthly_limit;
```

- Frecuencias: `MONTHLY`, `DAILY`, `WEEKLY`, `YEARLY`, `NEVER`.

### 2.7 Conectividad y Seguridad

| Método | Descripción |
|---|---|
| **MFA** | Multi-Factor Authentication |
| **SSO (SAML)** | Single Sign-On con proveedor de identidad |
| **OAuth** | Autorización para aplicaciones |
| **Key Pair Auth** | Par de llaves RSA para autenticación |
| **Private Link** | Conexión sin internet (AWS/Azure/GCP) |
| **AWS PrivateLink** | IPs privadas en AWS |
| **Azure Private Link** | Private Endpoint en Azure |
| **GC PSC** | Private Service Connect en GCP |

### 2.8 Replicación y Failover

- **Replication Groups:** Replican objetos entre regiones/cuentas.
- **Failover:** Promover réplica a principal (manual o automatizable).
- **Database Replication:** Replica objetos de base de datos.

```sql
ALTER DATABASE my_db ENABLE REPLICATION TO ACCOUNTS my_org.second_account;
```

### 2.9 Seguridad a nivel de objeto

- Privilegios: `USAGE`, `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `REFERENCES`.
- `OWNERSHIP`: solo un rol puede tener ownership (se transfiere).
- Roles secundarios: `SET SECONDARY ROLES ALL`.

### 2.10 Políticas de Datos (adicional)

- **Tag-based masking:** Aplicar masking policies mediante etiquetas.
- **Data Classification:** Clasificar datos automáticamente con Cortex AI.

---

## Dominio 3 — Carga y Descarga de Datos y Conectividad (18%)

### 3.1 Stages

| Tipo | Referencia | Descripción |
|---|---|---|
| **User Stage** | `@~` | Automático por usuario |
| **Table Stage** | `@%table_name` | Automático por tabla |
| **Named Stage (Interno)** | `@my_stage` | Almacenamiento en Snowflake |
| **Named Stage (Externo)** | `@ext_stage` | Apunta a S3/GCS/Azure |

```sql
LIST @~;
LIST @%my_table;
CREATE STAGE my_stage;
CREATE STAGE ext_stage URL='s3://bucket/path/' CREDENTIALS=(...);
REMOVE @my_stage;
```

- Los datos **no estructurados** (PDFs, imágenes) se almacenan en **stages internos o externos**, no en tablas.

### 3.2 COPY INTO (Carga)

```sql
COPY INTO my_table
FROM @my_stage
FILE_FORMAT = (TYPE = CSV SKIP_HEADER = 1);
```

- **Objetos necesarios:** Stage, Tabla y **Almacén Virtual** (warehouse).
- Carga datos desde archivos en un stage hacia una tabla existente.

### 3.3 Formatos de Archivo

| Formato | Tipo |
|---|---|
| CSV, JSON, Avro, Parquet, ORC, XML | Estructurados y semiestructurados |
| **JSON, Avro, ORC, Parquet** | Semiestructurados nativos |
| YAML, HTML, VCF | **NO** soportados nativamente |

```sql
CREATE FILE FORMAT json_fmt TYPE = JSON;
CREATE FILE FORMAT csv_fmt TYPE = CSV SKIP_HEADER = 1;
```

### 3.4 Datos Semiestructurados (FLATTEN)

| Tipo | Descripción |
|---|---|
| **VARIANT** | Almacena datos semiestructurados (JSON, etc.) |
| **OBJECT** | Pares clave-valor |
| **ARRAY** | Listas de valores |

```sql
SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('{"a":1,"b":2}')));
```

- `FLATTEN` descompone arrays/objetos en filas.
- La columna **VALUE** contiene el valor real del elemento.
- Otras columnas: `KEY`, `INDEX`, `SEQ`, `PATH`.

### 3.5 Datos No Estructurados (PARSE_DOCUMENT)

```sql
SELECT PARSE_DOCUMENT('@stage/reporte.pdf', 'PDF')::STRING AS contenido;
SELECT PARSE_DOCUMENT('@stage/doc.docx', 'DOCX')::STRING;
```

- Extrae texto de archivos PDF, DOCX, PPTX.
- Los archivos deben estar en un stage.

### 3.6 Snowpipe

Carga automatizada continua basada en eventos (SQS/SNS, GCS Pub/Sub, Azure Events).

```sql
CREATE PIPE my_pipe AS
  COPY INTO my_table
  FROM @my_stage
  FILE_FORMAT = (TYPE = JSON);

ALTER PIPE my_pipe REFRESH;  -- Carga manual de archivos existentes
```

### 3.7 Descarga de Datos (COPY INTO location)

```sql
COPY INTO @my_stage/data/
FROM my_table
FILE_FORMAT = (TYPE = PARQUET);
```

### 3.8 External Tables e Iceberg Tables

| Tipo | Almacenamiento | Mutabilidad |
|---|---|---|
| **External Table** | Datos en S3/GCS/Azure, metadatos en Snowflake | Solo lectura |
| **Iceberg Table** | Formato Apache Iceberg en almacenamiento externo | Lectura/escritura |

```sql
CREATE EXTERNAL TABLE ext_orders
  LOCATION = @ext_stage
  FILE_FORMAT = (TYPE = PARQUET);
```

---

## Dominio 4 — Optimización del Rendimiento, Consultas y Transformación (21%)

### 4.1 SQL Avanzado

| Concepto | Detalle |
|---|---|
| **SELECT \*** | Selecciona **todas las columnas** de una tabla |
| **LIMIT sin ORDER BY** | Resultado **no determinista** (no garantiza orden) |
| **CTEs** | Common Table Expressions con `WITH` |
| **JOINs** | INNER, LEFT, RIGHT, FULL OUTER |

```sql
WITH ventas_altas AS (
  SELECT * FROM orders WHERE amount > 1000
)
SELECT v.*, c.name
FROM ventas_altas v
JOIN customers c ON v.customer_id = c.id;
```

### 4.2 Funciones de Ventana

```sql
SELECT
  department,
  salary,
  ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) AS rank,
  LAG(salary) OVER (PARTITION BY dept ORDER BY salary) AS prev_salary,
  LEAD(salary) OVER (PARTITION BY dept ORDER BY salary) AS next_salary
FROM employees;
```

- `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LAG()`, `LEAD()`
- `SUM() OVER (PARTITION BY ... ORDER BY ...)`

### 4.3 Dynamic Tables

Se refrescan automáticamente según un `TARGET_LAG`.

```sql
CREATE DYNAMIC TABLE daily_sales
  TARGET_LAG = '5 minutes'
  WAREHOUSE = my_wh
  AS
  SELECT order_date, SUM(amount) AS total
  FROM orders
  GROUP BY order_date;
```

| Característica | Dynamic Table |
|---|---|
| Almacena datos | Sí |
| Actualización | Automática con target lag |
| Costo | Almacenamiento + mantenimiento |
| Uso típico | Pipelines ETL automatizados |

### 4.4 Materialized Views

| Feature | View estándar | Materialized View | Dynamic Table |
|---|---|---|---|
| **Almacena datos** | No | Sí | Sí |
| **Actualización** | Refleja tabla base | Auto-refresh con costo | Target lag configurable |
| **Costo** | Gratis | Almacenamiento + mantenimiento | Almacenamiento + mantenimiento |

```sql
CREATE MATERIALIZED VIEW mv_category
  AS SELECT category, COUNT(*) AS cnt
  FROM products
  GROUP BY category;
```

### 4.5 Tasks y Streams (CDC)

**Tasks:**
```sql
CREATE TASK process_orders
  WAREHOUSE = my_wh
  SCHEDULE = '5 MINUTE'
AS
  INSERT INTO order_log SELECT CURRENT_TIMESTAMP, COUNT(*) FROM orders;

CREATE TASK cleanup_task AFTER process_orders
  AS DELETE FROM temp_data;
```

- Se pueden encadenar con `AFTER`.
- Requieren warehouse o Snowflake-managed compute.

**Streams (CDC):**
```sql
CREATE STREAM order_changes ON TABLE orders;

SELECT * FROM order_changes;  -- INSERT, UPDATE, DELETE
```

- Captura cambios **INSERT, UPDATE, DELETE**.
- El offset avanza al consumir los datos (una vez leído, desaparece).
- Ideal para pipelines incrementales (Task + Stream).

### 4.6 EXPLAIN y Query Profile

```sql
EXPLAIN SELECT * FROM orders JOIN customers ON orders.cust_id = customers.id;
```

- **EXPLAIN:** Plan de ejecución textual.
- **Query Profile** (Snowsight): Identifica cuellos de botella (tablescans, joins costosos).
- **`USE_CACHED_RESULT = FALSE`** para pruebas sin cache.

### 4.7 Search Optimization Service

```sql
ALTER TABLE large_table ADD SEARCH OPTIMIZATION ON (search_col);
```

- Mejora búsquedas por punto y subcadenas.
- Costo adicional de almacenamiento.
- Útil en tablas grandes con búsquedas frecuentes.

### 4.8 Tipos de Datos

| Categoría | Tipos |
|---|---|
| **Semiestructurados** | VARIANT, OBJECT, ARRAY |
| **Geográficos** | GEOGRAPHY, GEOMETRY |
| **Numéricos** | NUMBER, INT, FLOAT |
| **Texto** | VARCHAR, STRING |
| **Binarios** | BINARY |
| **Fechas** | DATE, TIME, TIMESTAMP, TIMESTAMP_LTZ, TIMESTAMP_NTZ, TIMESTAMP_TZ |
| **Lógicos** | BOOLEAN |

- **VARCHAR** es el tipo recomendado para cadenas de texto grandes.

---

## Dominio 5 — Colaboración de Datos (10%)

### 5.1 Secure Data Sharing

- Comparte datos **sin copiarlos** (cero copia).
- El consumidor ve datos frescos sin réplicas.
- Las cuentas PRO solo pueden ser **consumidoras** de cuentas Standard.

```sql
CREATE SHARE sales_share;
GRANT USAGE ON DATABASE sales_db TO SHARE sales_share;
GRANT SELECT ON ALL TABLES IN SCHEMA sales_db.public TO SHARE sales_share;
ALTER SHARE sales_share ADD ACCOUNTS = org.consumer_account;
```

### 5.2 Reader Accounts

- Permiten compartir con cuentas que **no son Snowflake**.
- Solo lectura.
- Ideal para compartir con clientes/partners externos.

### 5.3 Marketplace vs Data Exchange

| Plataforma | Ámbito |
|---|---|
| **Snowflake Marketplace** | Público (cualquier cuenta Snowflake) |
| **Data Exchange** | Privado (dentro de una organización) |

- **No hay diferencia de rendimiento** entre ambos (usan Secure Data Sharing).

### 5.4 Auto-fulfillment

- Mecanismo de respaldo para que los datos estén disponibles aunque el provider esté en una región diferente.
- El consumidor no nota la diferencia.

---

## Apéndice A: Preguntas Frecuentes del Examen (Tipo Test)

Basado en las 30 preguntas del informe original y los temas de alta probabilidad:

1. **Vista previa tabla Snowsight:** Definición de la tabla + primeras 100 filas.
2. **COPY INTO:** Carga datos de stage a tabla.
3. **Interfaz web:** Snowsight.
4. **Time Travel default:** 1 día.
5. **Auto-suspend:** Reduce costos (apaga warehouse tras inactividad).
6. **COMPLETE:** Generar texto automáticamente.
7. **Celda verde notebook:** Ejecutada sin errores.
8. **Marketplace vs Data Exchange:** Mismo rendimiento.
9. **Botón Iniciar notebook:** Activa sesión de notebook.
10. **Almacenar datos:** Tabla.
11. **Texto grande:** VARCHAR.
12. **COPY INTO propósito:** Cargar datos de stage a tabla.
13. **LIMIT sin ORDER BY:** No determinista.
14. **Esquemas:** Contenidos en BD, organizan objetos.
15. **Cortex AI:** Extraer texto de no estructurados.
16. **Time Travel parámetro:** DATA_RETENTION_TIME_IN_DAYS.
17. **COPY INTO objetos:** Stage + Tabla + Warehouse.
18. **Notebook lenguajes:** SQL y Python.
19. **Historial consultas:** Query History en Snowsight.
20. **Datos no estructurados:** En stages.
21. **Acceso objetos:** Otorgar privilegios al rol.
22. **Procesamiento consulta:** Dimensionamiento de warehouses.
23. **Rol sistema:** USERADMIN.
24. **FLATTEN columna:** VALUE.
25. **PARSE_DOCUMENT:** Extraer texto de PDF.
26. **Acciones BD en Snowsight:** Renombrar y Eliminar.
27. **Cloud Services:** Metadatos.
28. **Semiestructurados:** ORC, Avro, JSON.
29. **Variable Python en SQL:** `{{myvar}}`.
30. **SELECT \*:** Todas las columnas de una tabla.

### Temas de alta probabilidad (no cubiertos en las 30 preguntas)

- Diferencia Time Travel vs Fail-safe
- Zero-copy cloning (alcance)
- Roles del sistema y herencia
- Ediciones (qué incluye cada una)
- Stages por defecto (`@~`, `@%table`)
- Caching (result cache no necesita warehouse)
- Clustering (depth, interval)
- Resource monitors y triggers
- Dynamic Tables vs Materialized Views vs Views

---

## Apéndice B: Badges DORA Recomendados

- **Insignia 1 — Data Warehousing:** Cubre Dominio 1 (arquitectura, tablas, cloning, time travel).
- **Insignia 2 — Collaboration, Marketplace & Cost:** Cubre Dominio 5 (data sharing) + Resource Monitors.
- **Insignia 4 — Data Lake:** Cubre Dominio 3 (stages, formatos, semiestructurados).
- **Insignia 5 — Data Engineering:** Cubre Dominio 4 (dynamic tables, streams, tasks, clustering).

**Orden recomendado:** Insignia 1 → Insignia 2 → Insignia 5 → Insignia 4.

---

## Apéndice C: Comandos SQL Clave para el Examen

```sql
-- Time Travel
SELECT * FROM t AT(TIMESTAMP => '...');
ALTER TABLE t SET DATA_RETENTION_TIME_IN_DAYS = 5;

-- Cloning
CREATE TABLE t2 CLONE t1;
CREATE TABLE t3 CLONE t1 AT(TIMESTAMP => '...');

-- Warehouses
CREATE WAREHOUSE w WITH WAREHOUSE_SIZE = 'SMALL' AUTO_SUSPEND = 5 AUTO_RESUME = TRUE;

-- Stages
CREATE STAGE s;
LIST @~;
COPY INTO t FROM @s FILE_FORMAT = (TYPE = CSV);

-- Data Sharing
CREATE SHARE s;
GRANT SELECT ON TABLE t TO SHARE s;

-- Governance
CREATE MASKING POLICY p AS (val STRING) RETURNS STRING -> CASE WHEN ... THEN val ELSE '***' END;
CREATE RESOURCE MONITOR m WITH CREDIT_QUOTA = 100 TRIGGERS ON 100% DO SUSPEND;

-- Dynamic Tables
CREATE DYNAMIC TABLE dt TARGET_LAG = '5 min' AS SELECT ...;

-- Streams + Tasks
CREATE STREAM st ON TABLE t;
CREATE TASK tk WAREHOUSE = w SCHEDULE = '5 min' AS INSERT INTO log SELECT * FROM st;

-- FLATTEN
SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('...')));

-- EXPLAIN
EXPLAIN SELECT ...;
```
