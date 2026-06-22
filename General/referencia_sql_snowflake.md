# Referencia SQL Snowflake — COF-C03

> Compendio de sintaxis SQL para Snowflake organizado por categorías.
> Basado en la documentación oficial y material de estudio SnowPro Core.

---

## 1. Consultas (SELECT)

### 1.1 SELECT básico

```sql
SELECT columna1, columna2
FROM tabla;
```

### 1.2 Funciones de cadena

```sql
SELECT INITCAP(pizza_type_id) AS capitalized_pizza_id FROM pizza_type;
SELECT UPPER(nombre) AS nombre_mayuscula FROM clientes;
SELECT LOWER(email) AS email_minuscula FROM usuarios;
SELECT CONCAT(nombre, ' ', apellido) AS nombre_completo FROM empleados;
SELECT CONCAT(name, ' - ', category) AS name_and_category FROM pizza_type;
SELECT SUBSTR(descripcion, 1, 10) AS resumen FROM productos;
SELECT TRIM('  texto  ') AS limpio;
SELECT REPLACE(telefono, '-', '') AS telefono_limpio FROM contactos;
SELECT LENGTH(codigo) AS longitud FROM referencias;
SELECT SPLIT(direccion, ',') AS partes_direccion FROM domicilios;
```

### 1.3 Funciones de fecha

```sql
SELECT CURRENT_DATE, CURRENT_TIME;
SELECT CURRENT_DATE;
SELECT CURRENT_TIMESTAMP;
SELECT DATEADD(day, 7, fecha_pedido) AS fecha_vencimiento FROM pedidos;
SELECT DATEDIFF(day, fecha_inicio, fecha_fin) AS dias FROM periodos;
SELECT DATE_TRUNC(month, fecha) AS mes FROM ventas;
SELECT EXTRACT(year FROM fecha_pedido) AS año FROM pedidos;
SELECT COUNT(*) AS orders_per_day,
       EXTRACT(weekday FROM order_date) AS order_day
FROM orders
GROUP BY order_day
ORDER BY orders_per_day DESC;
SELECT LAST_DAY(fecha) AS fin_mes FROM calendario;
```

### 1.4 Funciones de agregación

```sql
SELECT COUNT(*) AS total FROM clientes;
SELECT SUM(monto) AS ingresos_totales FROM ventas;
SELECT AVG(calificacion) AS promedio FROM evaluaciones;
SELECT MIN(precio) AS mas_barato, MAX(precio) AS mas_caro FROM productos;
SELECT categoria, COUNT(*) AS cantidad FROM productos GROUP BY categoria;
SELECT categoria, SUM(stock) AS total_stock FROM productos GROUP BY categoria HAVING total_stock > 100;
```

### 1.5 JOINs

```sql
SELECT c.nombre, p.monto
FROM clientes c
INNER JOIN pagos p ON c.id = p.cliente_id;

-- JOIN con USING (columna con mismo nombre)
SELECT EXTRACT(month FROM order_date) AS order_month,
       p.pizza_size,
       SUM(p.price * od.quantity) AS revenue
FROM orders o
INNER JOIN order_details od USING(order_id)
INNER JOIN pizzas p USING(pizza_id)
GROUP BY ALL
ORDER BY revenue DESC;

SELECT c.nombre, p.monto
FROM clientes c
LEFT JOIN pagos p ON c.id = p.cliente_id;

SELECT c.nombre, p.monto
FROM clientes c
RIGHT JOIN pagos p ON c.id = p.cliente_id;

SELECT c.nombre, p.monto
FROM clientes c
FULL OUTER JOIN pagos p ON c.id = p.cliente_id;

-- NATURAL JOIN: empareja columnas con mismo nombre, sin ON
SELECT pizza_type_id, name, category
FROM pizzas
NATURAL JOIN pizza_type;
-- Evita columnas duplicadas (no aparece pizza_type_id dos veces)

-- NATURAL JOIN con filtro WHERE
SELECT pizza_type_id, name, category
FROM pizzas
NATURAL JOIN pizza_type
WHERE category = 'Classic';

-- NATURAL JOIN cadena: order_details → pizzas → pizza_type
SELECT pt.category,
       SUM(p.price * od.quantity) AS total_revenue
FROM order_details AS od
NATURAL JOIN pizzas AS p
NATURAL JOIN pizza_type AS pt
GROUP BY pt.category
ORDER BY total_revenue DESC
LIMIT 5;

-- LATERAL JOIN: subconsulta accede a columnas de tabla anterior
SELECT p.pizza_id, pt.name, pt.category
FROM pizzas p,
LATERAL (SELECT * FROM pizza_type pt WHERE pt.pizza_type_id = p.pizza_type_id) pt;

-- LATERAL JOIN: ejemplo con cálculo por pedido
SELECT o.order_id, t.total_cost
FROM orders o,
LATERAL (SELECT SUM(p.price * od.quantity) AS total_cost
         FROM order_details od
         JOIN pizzas p ON od.pizza_id = p.pizza_id
         WHERE od.order_id = o.order_id) t;
```

### 1.6 CTEs (WITH)

```sql
WITH ventas_altas AS (
    SELECT cliente_id, SUM(monto) AS total
    FROM pagos
    GROUP BY cliente_id
    HAVING total > 1000
)
SELECT c.nombre, v.total
FROM clientes c
JOIN ventas_altas v ON c.id = v.cliente_id;
```

### 1.7 SELECT *

```sql
SELECT * FROM clientes;  -- Todas las columnas
SELECT v.*, c.nombre FROM ventas v JOIN clientes c ON v.cliente_id = c.id;
```

### 1.8 LIMIT y ORDER BY

```sql
SELECT nombre, salario
FROM empleados
ORDER BY salario DESC
LIMIT 10;  -- Top 10

-- LIMIT sin ORDER BY = resultado no determinista
SELECT * FROM eventos LIMIT 5;  -- Puede devolver filas diferentes cada vez
```

### 1.9 Datos semiestructurados (VARIANT)

```sql
SELECT columna:campo::STRING AS valor FROM tabla_json;
SELECT columna:objeto.campo::INT AS numero FROM tabla_json;
SELECT columna[0]::STRING AS primer_elemento FROM tabla_array;

SELECT * FROM TABLE(FLATTEN(INPUT => PARSE_JSON('{"a":1,"b":2}')));
/*
  Value columns: SEQ, KEY, PATH, INDEX, VALUE, THIS
  VALUE contiene el dato real desanidado
*/
```

### 1.10 Funciones de ventana

```sql
SELECT nombre, departamento, salario,
       ROW_NUMBER() OVER (PARTITION BY departamento ORDER BY salario DESC) AS ranking
FROM empleados;

SELECT fecha, monto,
       SUM(monto) OVER (ORDER BY fecha) AS acumulado
FROM ventas;

SELECT nombre, salario, departamento,
       RANK() OVER (PARTITION BY departamento ORDER BY salario DESC) AS rango
FROM empleados;

SELECT nombre, salario, departamento,
       LAG(salario) OVER (PARTITION BY departamento ORDER BY salario) AS salario_anterior,
       LEAD(salario) OVER (PARTITION BY departamento ORDER BY salario) AS salario_siguiente
FROM empleados;

SELECT departamento,
       AVG(salario) OVER (PARTITION BY departamento) AS promedio_dept
FROM empleados;
```

---

## 2. DDL — Creación y modificación de objetos

### 2.1 Bases de datos y esquemas

```sql
CREATE DATABASE mi_bd;
CREATE SCHEMA mi_bd.mi_esquema;
CREATE SCHEMA mi_esquema;  -- Usa BD del contexto actual
USE DATABASE mi_bd;
USE SCHEMA mi_bd.mi_esquema;
DROP DATABASE mi_bd;
DROP SCHEMA mi_bd.mi_esquema;
```

### 2.2 Tablas

```sql
CREATE TABLE clientes (
    id INT AUTOINCREMENT,
    nombre STRING(100),
    email STRING,
    fecha_registro DATE,
    activo BOOLEAN DEFAULT TRUE
);

CREATE OR REPLACE TABLE clientes AS SELECT * FROM clientes_temp;

-- Tipos de tabla
CREATE PERMANENT TABLE p (id INT);     -- Durable, 1-90d Time Travel
CREATE TRANSIENT TABLE t (id INT);     -- Durable, max 1d Time Travel
CREATE TEMPORARY TABLE tmp (id INT);   -- Solo sesión, max 1d Time Travel

-- Clonación zero-copy
CREATE TABLE t2 CLONE t1;
CREATE SCHEMA s2 CLONE s1;
CREATE DATABASE d2 CLONE d1;
CREATE TABLE t3 CLONE t1 AT(TIMESTAMP => '2026-07-01');

-- Clustering
CREATE TABLE pedidos (id INT, cliente_id INT, fecha DATE, monto NUMBER)
CLUSTER BY (cliente_id, fecha);

ALTER TABLE pedidos CLUSTER BY (cliente_id, fecha);
ALTER TABLE pedidos DROP CLUSTERING KEY;
```

### 2.3 Vistas

```sql
CREATE VIEW clientes_activos AS
SELECT id, nombre FROM clientes WHERE activo = TRUE;

CREATE SECURE VIEW clientes_anonymized AS
SELECT id, '***' AS nombre, SUBSTR(email, 1, 3) || '@...' AS email FROM clientes;

CREATE MATERIALIZED VIEW mv_categoria AS
SELECT categoria, COUNT(*) AS cantidad
FROM productos
GROUP BY categoria;
```

### 2.4 Dynamic Tables

```sql
CREATE DYNAMIC TABLE daily_sales
TARGET_LAG = '5 minutes'
WAREHOUSE = my_wh
AS
SELECT order_date, SUM(amount) AS total
FROM orders
GROUP BY order_date;
```

### 2.5 Tablas externas

```sql
CREATE EXTERNAL TABLE ext_orders
LOCATION = @ext_stage
FILE_FORMAT = (TYPE = PARQUET);
```

---

## 3. DML — Manipulación de datos

```sql
INSERT INTO clientes (nombre, email) VALUES ('Juan Pérez', 'juan@email.com');
INSERT INTO clientes SELECT * FROM clientes_backup;

UPDATE clientes SET activo = FALSE WHERE id = 1;

DELETE FROM clientes WHERE activo = FALSE;

MERGE INTO clientes c
USING clientes_actualizados a ON c.id = a.id
WHEN MATCHED THEN UPDATE SET c.nombre = a.nombre, c.email = a.email
WHEN NOT MATCHED THEN INSERT (id, nombre, email) VALUES (a.id, a.nombre, a.email);

TRUNCATE TABLE clientes;
DROP TABLE clientes;
```

---

## 4. DCL — Control de acceso

### 4.1 Roles

```sql
CREATE ROLE analyst;
CREATE ROLE data_engineer;
CREATE ROLE access_read;

-- Jerarquía
GRANT ROLE access_read TO ROLE analyst;
GRANT ROLE analyst TO ROLE data_engineer;
GRANT ROLE data_engineer TO ROLE sysadmin;

-- Asignar a usuario
GRANT ROLE analyst TO USER usuario1;

SET SECONDARY ROLES ALL;  -- Activar roles secundarios en sesión
```

### 4.2 Privilegios

```sql
GRANT USAGE ON DATABASE mi_bd TO ROLE analyst;
GRANT USAGE ON SCHEMA mi_bd.mi_esquema TO ROLE analyst;
GRANT SELECT ON ALL TABLES IN SCHEMA mi_bd.mi_esquema TO ROLE analyst;
GRANT SELECT ON FUTURE TABLES IN SCHEMA mi_bd.mi_esquema TO ROLE analyst;
GRANT INSERT, UPDATE ON TABLE mi_bd.mi_esquema.pedidos TO ROLE analyst;
GRANT ALL PRIVILEGES ON WAREHOUSE mi_wh TO ROLE analyst;

REVOKE SELECT ON TABLE mi_bd.mi_esquema.clientes FROM ROLE analyst;
```

---

## 5. Time Travel y Fail-safe

```sql
-- Consultas históricas
SELECT * FROM table AT(TIMESTAMP => '2026-07-01 10:00:00');
SELECT * FROM table BEFORE(STATEMENT => '019a8b50-...');
SELECT * FROM table AT(OFFSET => -300);  -- 5 minutos atrás

-- Configurar retención
ALTER TABLE table SET DATA_RETENTION_TIME_IN_DAYS = 3;
ALTER TABLE table SET DATA_RETENTION_TIME_IN_DAYS = 90;  -- Enterprise+

-- Restaurar objetos eliminados
UNDROP TABLE table;
UNDROP SCHEMA schema;
UNDROP DATABASE database;
```

---

## 6. Clonación Zero-Copy

```sql
-- Clon completo
CREATE TABLE copia CLONE original;
CREATE SCHEMA copia_schema CLONE original_schema;
CREATE DATABASE copia_bd CLONE original_bd;

-- Clon en punto temporal
CREATE TABLE copia CLONE original AT(TIMESTAMP => '2026-07-01 12:00:00');

-- Clon con Time Travel relativo
CREATE TABLE copia CLONE original AT(OFFSET => -3600);
```

---

## 7. Stages y carga de datos

### 7.1 Stages

```sql
-- Tipos de stage
LIST @~;            -- User stage
LIST @%table_name;  -- Table stage
LIST @named_stage;  -- Named stage

-- Crear stages
CREATE STAGE mi_stage;  -- Interno
CREATE STAGE ext_stage
  URL = 's3://bucket/path/'
  STORAGE_INTEGRATION = mi_integracion
  FILE_FORMAT = (TYPE = CSV);

CREATE STAGE ext_stage_azure
  URL = 'azure://storage.blob.core.windows.net/container/path/'
  CREDENTIALS = (AZURE_SAS_TOKEN = '...');

CREATE STAGE ext_stage_gcp
  URL = 'gcs://bucket/path/';

DROP STAGE mi_stage;
```

### 7.2 COPY INTO (Carga)

```sql
COPY INTO mi_tabla
FROM @mi_stage
FILE_FORMAT = (TYPE = CSV SKIP_HEADER = 1);

COPY INTO mi_tabla (col1, col2)
FROM @mi_stage/data/
FILE_FORMAT = (TYPE = JSON STRIP_OUTER_ARRAY = TRUE);

-- Validación (sin cargar)
COPY INTO mi_tabla
FROM @mi_stage
VALIDATION_MODE = RETURN_ERRORS;
```

### 7.3 COPY INTO (Descarga)

```sql
COPY INTO @mi_stage/data/
FROM mi_tabla
FILE_FORMAT = (TYPE = PARQUET);

COPY INTO @mi_stage/report.csv
FROM (SELECT id, nombre, fecha FROM clientes WHERE activo = TRUE)
FILE_FORMAT = (TYPE = CSV HEADER = TRUE);
```

### 7.4 Formatos de archivo

```sql
CREATE FILE FORMAT csv_fmt
  TYPE = CSV
  SKIP_HEADER = 1
  FIELD_OPTIONALLY_ENCLOSED_BY = '"';

CREATE FILE FORMAT json_fmt
  TYPE = JSON
  STRIP_OUTER_ARRAY = TRUE;

CREATE FILE FORMAT parquet_fmt
  TYPE = PARQUET;

CREATE FILE FORMAT avro_fmt
  TYPE = AVRO;
```

### 7.5 Snowpipe

```sql
CREATE PIPE mi_pipe AS
  COPY INTO mi_tabla
  FROM @mi_stage
  FILE_FORMAT = (TYPE = CSV SKIP_HEADER = 1);

-- Carga manual de archivos existentes
ALTER PIPE mi_pipe REFRESH;

-- Pausar/reanudar
ALTER PIPE mi_pipe SET PIPE_EXECUTION_PAUSED = TRUE;
ALTER PIPE mi_pipe SET PIPE_EXECUTION_PAUSED = FALSE;

DROP PIPE mi_pipe;
```

### 7.6 Datos no estructurados

```sql
SELECT PARSE_DOCUMENT('@stage/reporte.pdf', 'PDF')::STRING AS contenido;
SELECT PARSE_DOCUMENT('@stage/doc.docx', 'DOCX')::STRING AS texto;

-- Directorio de stage
ALTER STAGE mi_stage SET DIRECTORY = (ENABLE = TRUE);
```

---

## 8. Warehouses

```sql
CREATE WAREHOUSE mi_wh
  WAREHOUSE_SIZE = 'XSMALL'       -- XSMALL a 6X-LARGE
  AUTO_SUSPEND = 5                -- Minutos de inactividad
  AUTO_RESUME = TRUE
  MIN_CLUSTER_COUNT = 1
  MAX_CLUSTER_COUNT = 3           -- Multi-cluster
  SCALING_POLICY = 'STANDARD'     -- o 'ECONOMY'
  INITIALLY_SUSPENDED = TRUE;

ALTER WAREHOUSE mi_wh SET WAREHOUSE_SIZE = 'SMALL';
ALTER WAREHOUSE mi_wh SUSPEND;
ALTER WAREHOUSE mi_wh RESUME;
DROP WAREHOUSE mi_wh;
```

---

## 9. Tasks y Streams

### 9.1 Streams (CDC)

```sql
CREATE STREAM cambios_pedidos ON TABLE pedidos;
CREATE STREAM cambios_pedidos_append ON TABLE pedidos SHOW_INITIAL_ROWS = TRUE;

-- Consultar cambios
SELECT * FROM cambios_pedidos;
-- Columnas: METADATA$ACTION (INSERT/UPDATE/DELETE), METADATA$ISUPDATE, METADATA$ROW_ID

DROP STREAM cambios_pedidos;
```

### 9.2 Tasks

```sql
CREATE TASK procesar_pedidos
  WAREHOUSE = mi_wh
  SCHEDULE = '5 MINUTE'
AS
  INSERT INTO log_pedidos SELECT * FROM cambios_pedidos;

-- Tasks encadenadas
CREATE TASK limpiar_temp
  AFTER procesar_pedidos
AS
  DELETE FROM pedidos_temp WHERE procesado = TRUE;

-- Control
ALTER TASK procesar_pedidos RESUME;
ALTER TASK procesar_pedidos SUSPEND;
DROP TASK procesar_pedidos;
```

---

## 10. Gobernanza y seguridad

### 10.1 Masking Policies

```sql
CREATE MASKING POLICY email_mask AS (val STRING) RETURNS STRING ->
  CASE
    WHEN CURRENT_ROLE() IN ('ADMIN') THEN val
    ELSE '***'
  END;

ALTER TABLE usuarios MODIFY COLUMN email SET MASKING POLICY email_mask;
ALTER TABLE usuarios MODIFY COLUMN email UNSET MASKING POLICY;
DROP MASKING POLICY email_mask;
```

### 10.2 Row Access Policies

```sql
CREATE ROW ACCESS POLICY region_filter AS (region STRING) RETURNS BOOLEAN ->
  CURRENT_ROLE() IN ('ADMIN', 'GLOBAL') OR region = 'PUBLIC';

ALTER TABLE ventas ADD ROW ACCESS POLICY region_filter ON (region);
ALTER TABLE ventas DROP ROW ACCESS POLICY region_filter;
DROP ROW ACCESS POLICY region_filter;
```

### 10.3 Network Policies

```sql
CREATE NETWORK RULE red_oficina
  TYPE = IPV4
  VALUE_LIST = ('192.168.1.0/24', '10.0.0.0/8');

CREATE NETWORK POLICY politica_red
  ALLOWED_NETWORK_RULE_LIST = ('red_oficina')
  BLOCKED_NETWORK_RULE_LIST = ();

ALTER ACCOUNT SET NETWORK POLICY = politica_red;
ALTER ACCOUNT UNSET NETWORK POLICY;

DROP NETWORK POLICY politica_red;
```

### 10.4 Resource Monitors

```sql
CREATE RESOURCE MONITOR limite_mensual
  WITH
    CREDIT_QUOTA = 100
    FREQUENCY = MONTHLY          -- MONTHLY | DAILY | WEEKLY | YEARLY | NEVER
    START_TIMESTAMP = '2026-07-01'
  TRIGGERS
    ON 80% DO NOTIFY
    ON 100% DO SUSPEND
    ON 110% DO SUSPEND_IMMEDIATE;

ALTER WAREHOUSE mi_wh SET RESOURCE_MONITOR = limite_mensual;
ALTER RESOURCE MONITOR limite_mensual SET CREDIT_QUOTA = 200;
DROP RESOURCE MONITOR limite_mensual;
```

### 10.5 Object Tagging

```sql
CREATE TAG sensibilidad ALLOWED_VALUES 'PII', 'CONFIDENTIAL', 'PUBLIC';
ALTER TABLE clientes MODIFY COLUMN email SET TAG sensibilidad = 'PII';
ALTER TABLE clientes MODIFY COLUMN nombre SET TAG sensibilidad = 'PUBLIC';

SELECT * FROM TABLE(INFORMATION_SCHEMA.TAG_REFERENCES('clientes', 'TABLE'));
```

### 10.6 Alertas

```sql
CREATE ALERT notificar_alta_demanda
  WAREHOUSE = mi_wh
  SCHEDULE = '10 MINUTE'
  IF (EXISTS (SELECT 1 FROM metricas WHERE uso_cpu > 90))
  THEN
    CALL SYSTEM$SEND_SNOWFLAKE_NOTIFICATION(
      '{"message":"Alto uso de CPU detectado"}'
    );
```

### 10.7 Cifrado y replicación

```sql
-- Replicación
ALTER DATABASE mi_bd ENABLE REPLICATION TO ACCOUNTS org.cuenta_secundaria;

-- Failover groups (Enterprise+)
CREATE FAILOVER GROUP mi_grupo
  OBJECT_TYPES = DATABASES, WAREHOUSES, ROLES
  ALLOWED_DATABASES = mi_bd
  ALLOWED_ACCOUNTS = org.cuenta_secundaria;
```

---

## 11. Colaboración y Data Sharing

### 11.1 Secure Data Sharing

```sql
-- Proveedor
CREATE SHARE ventas_share;
GRANT USAGE ON DATABASE mi_bd TO SHARE ventas_share;
GRANT USAGE ON SCHEMA mi_bd.public TO SHARE ventas_share;
GRANT SELECT ON TABLE mi_bd.public.ventas TO SHARE ventas_share;
ALTER SHARE ventas_share ADD ACCOUNTS = org.consumidor;

-- Consumidor
CREATE DATABASE ventas_compartidas FROM SHARE org.proveedor.ventas_share;

DROP SHARE ventas_share;
```

### 11.2 Reader Accounts

```sql
-- Crear cuenta lector para socios sin Snowflake
CREATE MANAGED ACCOUNT socio_reader
  ADMIN_NAME = 'admin_socio'
  ADMIN_PASSWORD = 'ContraseñaSegura!'
  TYPE = READER;

ALTER SHARE ventas_share ADD ACCOUNTS = org.socio_reader;
```

---

## 12. Monitoreo y optimización

### 12.1 EXPLAIN y Query Profile

```sql
EXPLAIN SELECT * FROM pedidos JOIN clientes ON pedidos.cliente_id = clientes.id;

-- Forzar sin caché para pruebas
ALTER SESSION SET USE_CACHED_RESULT = FALSE;
```

### 12.2 Metadatos de clustering

```sql
SELECT SYSTEM$CLUSTERING_DEPTH('pedidos');
SELECT SYSTEM$CLUSTERING_INTERVAL('pedidos', 'fecha');
SELECT SYSTEM$CLUSTERING_INFORMATION('pedidos');
```

### 12.3 Search Optimization

```sql
ALTER TABLE pedidos ADD SEARCH OPTIMIZATION;
ALTER TABLE pedidos ADD SEARCH OPTIMIZATION ON (cliente_id, email);
```

### 12.4 Information Schema y Account Usage

```sql
SELECT * FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA = 'PUBLIC';

-- Account Usage (mayor latencia, más histórico)
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.QUERY_HISTORY
WHERE USER_NAME = 'USUARIO1'
ORDER BY START_TIME DESC
LIMIT 100;

SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.WAREHOUSE_METERING_HISTORY;
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.STORAGE_USAGE;
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.GRANTS_TO_ROLES;

SHOW TABLES;
SHOW SCHEMAS;
SHOW WAREHOUSES;
SHOW ROLES;
SHOW GRANTS TO ROLE analyst;
SHOW FUTURE GRANTS TO ROLE analyst;
DESCRIBE TABLE clientes;
```

---

## 13. Notebooks y Cortex AI

```sql
-- Notebook: celda SQL referenciando variable Python
SELECT '{{myvar}}' AS resultado;

-- Cortex AI
SELECT COMPLETE('snowflake-arctic', 'Resume: Snowflake es una plataforma...') AS resumen;

-- Celda verde = ejecutada sin errores
```

---

## 14. Funciones de sistema útiles

```sql
SELECT CURRENT_ROLE();
SELECT CURRENT_USER();
SELECT CURRENT_DATABASE();
SELECT CURRENT_SCHEMA();
SELECT CURRENT_WAREHOUSE();
SELECT CURRENT_ACCOUNT();
SELECT CURRENT_REGION();
SELECT CURRENT_VERSION();

SELECT SYSTEM$TYPEOF(valor_variant);
SELECT SYSTEM$CLUSTERING_DEPTH('tabla');
SELECT PARSE_JSON('{"clave": "valor"}');
SELECT TRY_PARSE_JSON('{"invalido"}');  -- NULL si no es JSON válido
SELECT HASH('*');  -- Hash de todas las columnas de una tabla
```

---

## 15. Convenciones y buenas prácticas

| Regla | Detalle |
|---|---|
| **Mayúsculas** | Palabras reservadas en mayúsculas (SELECT, FROM, WHERE) |
| **Punto y coma** | Toda sentencia termina en `;` |
| **Comentarios** | `--` para línea, `/* */` para bloque |
| **Nombres de objetos** | Sin espacios, usar snake_case |
| **Comillas dobles** | Para identificadores con caracteres especiales: `"Mi Tabla"` |
| **Contexto** | USE DATABASE + USE SCHEMA antes de operar |

---

> Archivo generado a partir de apuntes SnowPro Core COF-C03.
> Fuentes: `apuntes_snowpro_core.md`, `guia_dora_badges.md`, `informe_snowflake.md`, y documentación oficial Snowflake.
