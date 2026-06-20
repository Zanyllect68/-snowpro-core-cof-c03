# Plan de Estudio - SnowPro Core Certification

> Complemento al informe de preguntas 01-30. Enfocado en los temas que NO aparecieron en ese conjunto.

---

## 1. Microparticiones y Clustering

| Concepto | Detalle |
|---|---|
| **¿Qué son?** | Unidades inmutables de ~50-500 MB comprimidos. Subyacentes a las tablas. |
| **Partition pruning** | Snowflake automáticamente elimina microparticiones irrelevantes usando metadatos (min/max, null count). |
| **Clustering keys** | Opcional. Ayuda en tablas grandes (>1 TB) con filtros por columnas específicas. |
| **Auto-clustering** | Servicio gestionado que reordena microparticiones (costo adicional). |
| **Profundidad de clúster** | Métrica que indica cuántas microparticiones se deben escanear. |

**Ejemplo:**
```sql
ALTER TABLE orders CLUSTER BY (customer_id, order_date);
SELECT SYSTEM$CLUSTERING_DEPTH('orders');
SELECT SYSTEM$CLUSTERING_INTERVAL('orders', 'order_date');
```

---

## 2. Caching

| Tipo de Cache | Alcance | Duración |
|---|---|---|
| **Result Cache** | Consultas repetidas | 24 horas (o hasta que cambien los datos subyacentes) |
| **Query Cache** | A nivel de warehouse | Mientras el warehouse esté activo |
| **Metadata Cache** | En Cloud Services | Siempre disponible (sin warehouse necesario) |
| **Local Disk Cache (SSD)** | En nodos del warehouse | Mientras el warehouse esté activo |

**Nota clave:** El result cache NO requiere un warehouse funcionando para servirse.

---

## 3. Clonación Zero-Copy

```sql
CREATE TABLE table_clone CLONE source_table;
```

- No copia datos físicamente; solo metadatos.
- Instantánea (inmediata, sin costo de almacenamiento adicional hasta que se modifiquen datos).
- Funciona con esquemas y bases de datos completas.
- La clonación **time-travel** permite clonar desde un punto anterior:
  ```sql
  CREATE TABLE table_restored CLONE my_table
    AT (TIMESTAMP => '2024-01-01 10:00:00');
  ```

---

## 4. Fail-safe

| Aspecto | Detalle |
|---|---|
| **Duración** | 7 días (fijo, NO configurable) |
| **Propósito** | Recuperación de desastres (solo Snowflake puede acceder) |
| **Costo** | Incluido en el almacenamiento (no hay cobro extra explícito, pero consume espacio) |
| **Acceso** | Solo el equipo de Snowflake puede recuperar datos en fail-safe |
| **Diferencia con Time Travel** | Time Travel: configurable (0-90 días). Fail-safe: 7 días fijos después de Time Travel |

**Línea de tiempo:**
```
Tabla activa → Time Travel (1-90 días) → Fail-safe (7 días) → Datos eliminados permanentemente
```

---

## 5. Tablas Temporales y Transitorias

| Tipo | Duración | Persistencia | Time Travel |
|---|---|---|---|
| **Permanente** | Indefinida | Sí | 1-90 días |
| **Transitoria** | Indefinida | Sí | 1 día (máximo) |
| **Temporal** | Sesión | No (se elimina al cerrar sesión) | 1 día (máximo) |

```sql
CREATE TRANSIENT TABLE my_transient (id INT);
CREATE TEMPORARY TABLE my_temp (id INT);
```

---

## 6. Stages

| Tipo de Stage | Descripción |
|---|---|
| **User Stage** | Automático para cada usuario (`@~`) |
| **Table Stage** | Automático para cada tabla (`@%table_name`) |
| **Named Stage (Interno)** | Creado explícitamente, almacena archivos en Snowflake |
| **Named Stage (Externo)** | Apunta a S3, GCS o Azure Blob |

```sql
CREATE STAGE my_stage;
CREATE STAGE external_stage URL='s3://bucket/path/' CREDENTIALS=(...);
LIST @my_stage;
REMOVE @my_stage;
```

---

## 7. Resource Monitors

```sql
CREATE RESOURCE MONITOR monthly_limit
  WITH CREDIT_QUOTA = 5000
  FREQUENCY = MONTHLY
  START_TIMESTAMP = '2024-01-01 00:00'
  TRIGGERS ON 80% DO NOTIFY
           ON 100% DO SUSPEND
           ON 110% DO SUSPEND_IMMEDIATE;
ALTER WAREHOUSE my_wh SET RESOURCE_MONITOR = monthly_limit;
```

- Operan a nivel de cuenta o warehouse.
- Acciones: `NOTIFY`, `SUSPEND`, `SUSPEND_IMMEDIATE`.
- Frecuencias: `MONTHLY`, `DAILY`, `WEEKLY`, `YEARLY`, `NEVER`.

---

## 8. Ediciones de Snowflake

| Edition | Características clave |
|---|---|
| **Standard** | Time Travel 1d, Fail-safe 7d, compartición de datos básica |
| **Enterprise** | Time Travel hasta 90d, Multi-cluster warehouses, Materialized views, ASO (Account-level Sharing Objects) |
| **Business Critical** | Todo lo de Enterprise + HIPAA, HITRUST, protección de datos a nivel de columna |
| **Virtual Private Snowflake (VPS)** | Todo lo de Business Critical + aislado con IP dedicada, Private Link, SOC2 Type 2 |

---

## 9. Materialized Views vs Views vs Dynamic Tables

| Feature | View estándar | Materialized View | Dynamic Table |
|---|---|---|---|
| **Almacena datos** | No | Sí | Sí |
| **Actualización automática** | No (refleja tabla base) | Auto-refresh con costo | Sí, con target lag configurable |
| **Costo** | Gratis | Almacenamiento + mantenimiento | Almacenamiento + mantenimiento |
| **Uso típico** | Simplificar consultas | Agregaciones pesadas en tablas grandes | ETL automatizado y pipelines |

---

## 10. Tareas (Tasks) y Streams

**Tasks:**
```sql
CREATE TASK my_task
  WAREHOUSE = my_wh
  SCHEDULE = '5 MINUTE'
AS
  INSERT INTO log_table SELECT CURRENT_TIMESTAMP;
```

- Se pueden encadenar (`AFTER`).
- Requieren un warehouse o Snowflake-managed compute.
- `EXECUTE TASK` manual o automático.

**Streams (CDC):**
```sql
CREATE STREAM my_stream ON TABLE source_table;
SELECT * FROM my_stream;  -- Muestra INSERT, UPDATE, DELETE
```

- `INSERT`, `UPDATE`, `DELETE` se registran.
- El consumo avanza el offset (una vez leído, desaparece).
- Ideal para pipelines incrementales (tarea + stream).

---

## 11. Roles y RBAC

| Rol | Descripción |
|---|---|
| `ORGADMIN` | Gestión a nivel de organización (crear cuentas) |
| `ACCOUNTADMIN` | Administración completa de la cuenta |
| `SECURITYADMIN` | Gestión de roles y usuarios |
| `USERADMIN` | Creación de usuarios y roles |
| `SYSADMIN` | Creación de objetos (warehouses, databases, etc.) |
| `PUBLIC` | Rol base que todos tienen |

**Herencia:** `ACCOUNTADMIN` > `SECURITYADMIN` > `USERADMIN` (vertical), y `ACCOUNTADMIN` > `SYSADMIN` (horizontal).

---

## 12. Políticas de Datos

| Política | Función |
|---|---|
| **Masking Policy** | Enmascarar columnas según el rol |
| **Row Access Policy** | Filtrar filas según el rol |
| **Network Policy** | Restringir IPs que pueden conectarse |
| **Tag-based masking** | Aplicar políticas mediante etiquetas |

```sql
CREATE MASKING POLICY email_mask AS (val STRING) RETURNS STRING ->
  CASE WHEN CURRENT_ROLE() IN ('ADMIN') THEN val ELSE '***' END;
ALTER TABLE users MODIFY COLUMN email SET MASKING POLICY email_mask;
```

---

## 13. Replicación y Failover

- **Replication Groups:** Replican objetos entre regiones/cuentas.
- **Failover:** Manual o automatizable (promover réplica a principal).
- **Database replication:** Replica objetos de base de datos.
- **Disaster Recovery:** Usando `ENABLE REPLICATION` + `REFRESH`.

```sql
ALTER DATABASE my_db ENABLE REPLICATION TO ACCOUNTS my_org.second_account;
```

---

## 14. External Tables e Iceberg Tables

| Tipo | Almacenamiento |
|---|---|
| **External Table** | Datos en S3/GCS/Azure, metadatos en Snowflake (solo lectura) |
| **Iceberg Table** | Formato Apache Iceberg, datos en almacenamiento externo, mutables |

```sql
CREATE EXTERNAL TABLE ext_orders
  LOCATION = @external_stage
  FILE_FORMAT = (TYPE = PARQUET);
```

---

## 15. Conectividad y Seguridad

- **Private Link** (AWS/Azure/GCP) — sin tráfico por internet.
- **AWS PrivateLink** — IPs privadas.
- **Azure Private Link** — Private Endpoint.
- **GC PSC** (Private Service Connect).
- **Key Pair Authentication** (par de llaves RSA).
- **OAuth** e **integraciones SAML** (SSO).
- **MFA** (Multi-Factor Authentication).

---

## 16. Seguridad a nivel de objeto

- `USAGE`, `SELECT`, `INSERT`, `UPDATE`, `DELETE`, `REFERENCES`
- `OWNERSHIP` (solo un rol puede tener ownership de un objeto)
- Roles secundarios: `SET SECONDARY ROLES ALL`

---

## 17. Tipos de Datos Completos

| Semiestructurados | Geográficos | Otros |
|---|---|---|
| VARIANT, OBJECT, ARRAY | GEOGRAPHY, GEOMETRY | NUMBER, FLOAT, VARCHAR, BINARY, DATE, TIME, TIMESTAMP |

---

## 18. Ventanas y Funciones Analíticas

```sql
ROW_NUMBER(), RANK(), DENSE_RANK(), LAG(), LEAD(),
SUM() OVER (PARTITION BY ... ORDER BY ...)
```

---

## 19. Optimización de Consultas

- **Search Optimization Service** — mejora búsquedas por punto y subcadenas en tablas grandes (costo adicional).
- **EXPLAIN** — plan de ejecución.
- **Query Profile** en Snowsight (identificar cuellos de botella).
- **Uso de `USE_CACHED_RESULT = FALSE`** para pruebas.

---

## 20. Data Sharing

- **Secure Data Sharing:** Sin copiar datos (cuentas PRO solo pueden ser consumidores de cuentas estándar).
- **Data Exchange:** Market privado dentro de una organización.
- **Snowflake Marketplace:** Público.
- **Reader Accounts:** Permiten compartir con cuentas que no son Snowflake (solo lectura).
- **Auto-fulfillment:** Disponibilidad alternativa si el provider no está en la misma región.

---

## 21. Penetración de Preguntas comunes

Temas con alta probabilidad de aparecer:
- Diferencia entre Time Travel y Fail-safe
- Zero-copy cloning (qué sí y qué no se clona)
- Comportamiento de `LIMIT` sin `ORDER BY`
- Roles del sistema y herencia
- Ediciones de Snowflake (qué incluye cada una)
- Parámetros de warehouse (`AUTO_SUSPEND`, `AUTO_RESUME`, `WAREHOUSE_SIZE`, `MULTI_CLUSTER`)
- Stages por defecto (`@~`, `@%table`)
- `FLATTEN` y sus columnas
- Tipos de tablas (permanente, transitoria, temporal)
- Resource monitors y triggers
- Data sharing (Reader Accounts)
- Clustering (depth, interval)
- Caching (result cache no necesita warehouse)

---

## Recursos recomendados

1. **Documentación oficial de Snowflake:** https://docs.snowflake.com/
2. **SnowPro Core Exam Guide** (publicado por Snowflake)
3. **Guía de estudio oficial:** https://learn.snowflake.com/
4. **Badge "Snowflake Fundamentals"** (gratuito en Snowflake University)
5. **Hands-on:** Crear una cuenta trial gratuita y practicar todos los conceptos.

---

> **Sugerencia:** Crea una cuenta trial y practica cada comando SQL listado aquí. El examen tiene preguntas prácticas sobre sintaxis y comportamiento.
