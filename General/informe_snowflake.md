# Informe - Preguntas y Respuestas Snowflake

## 01/30 — Vista previa de una tabla en Snowsight
**Pregunta:** ¿Qué información está disponible durante la vista previa de una tabla en Snowsight?

**Respuesta:** La definición de la tabla y las primeras 100 filas de la tabla.

**Explicación:**
- La **definición de la tabla** está disponible en la pestaña *Table Details*, sección *Table definition*.
- Las **primeras 100 filas** están disponibles en la pestaña *Data Preview*.
- El diagrama ER **no** se muestra en la vista previa.
- Las tablas no se almacenan en un *warehouse*; el warehouse solo se usa para ejecutar consultas.

---

## 02/30 — COPY INTO
**Pregunta:** ¿Qué ocurre cuando se ejecuta `COPY INTO table_2 FROM @stage_25;`?

**Respuesta:** Se cargan datos de stage_25 a table_2.

**Explicación:** `COPY INTO` carga datos desde una fase (stage) hacia una tabla existente.

---

## 03/30 — Interfaz web predeterminada
**Pregunta:** ¿Qué nombre tiene la interfaz basada en web predeterminada de Snowflake?

**Respuesta:** Snowsight.

**Explicación:** Snowsight es la interfaz web moderna de Snowflake. SnowSQL es la CLI, Snowpark es la librería de programación, y Snowflake CLI es la herramienta de línea de comandos.

---

## 04/30 — Time Travel
**Pregunta:** ¿Cuál es el período de retención de datos predeterminado de Time Travel?

**Respuesta:** 1 día.

**Explicación:** El valor predeterminado es 1 día (24 horas). Se puede configurar hasta 90 días para cuentas Enterprise.

---

## 05/30 — Suspensión automática
**Pregunta:** ¿Qué impacto tiene habilitar la suspensión automática en un almacén virtual?

**Respuesta:** El almacén dejará de funcionar después de un período específico de inactividad, lo que reduce los costos.

**Explicación:** Auto-suspend apaga el warehouse tras un periodo de inactividad configurable, evitando costos innecesarios.

---

## 06/30 — COMPLETE de Cortex LLM
**Pregunta:** ¿Para qué se usa la función COMPLETE de Snowflake Cortex LLM?

**Respuesta:** Para automatizar la generación de una respuesta de texto.

**Explicación:** `COMPLETE()` es una función de Cortex AI que genera texto a partir de un prompt usando modelos LLM.

---

## 07/30 — Estado de celda verde en Notebooks
**Pregunta:** ¿Qué indica un estado de celda en color verde constante en Snowflake Notebooks?

**Respuesta:** La celda se ejecutó en la sesión actual sin errores.

**Explicación:** En Snowflake Notebooks, el indicador verde significa ejecución exitosa; rojo indica error; naranja/amarillo indica modificación sin ejecución.

---

## 08/30 — Marketplace vs Data Exchange
**Pregunta:** ¿Cómo se compara el rendimiento de consulta de datos compartidos a través de Snowflake Marketplace con Data Exchange?

**Respuesta:** No hay diferencia en el rendimiento de la consulta de datos compartidos en Snowflake Marketplace con el rendimiento de la consulta de datos compartidos en Data Exchange.

**Explicación:** Ambos usan el mismo mecanismo de compartición (Secure Data Sharing); el rendimiento es idéntico.

---

## 09/30 — Botón Iniciar en Notebooks
**Pregunta:** ¿Cuál es el fin del botón Iniciar en la barra de tareas de Snowflake Notebooks?

**Respuesta:** Inicia una sesión de notebook y establece su etiqueta a activa cuando está lista.

**Explicación:** El botón Start activa el runtime del notebook para poder ejecutar celdas.

---

## 10/30 — Objeto para almacenar datos
**Pregunta:** ¿Qué objeto de Snowflake se usa para almacenar datos?

**Respuesta:** Tabla.

**Explicación:** Las tablas son el objeto principal para almacenar datos estructurados en Snowflake. Los almacenes virtuales son para cómputo, las vistas son consultas almacenadas, los procedimientos son código.

---

## 11/30 — Tipo de dato para texto grande
**Pregunta:** ¿Qué tipo de dato se recomienda para almacenar una cadena de texto grande en Snowflake?

**Respuesta:** VARCHAR.

**Explicación:** VARCHAR es el tipo de datos estándar para cadenas de texto en Snowflake. OBJECT y ARRAY son para semiestructurados, BOOLEAN es lógico.

---

## 12/30 — COPY INTO (propósito)
**Pregunta:** ¿Para qué se usa el comando SQL COPY INTO?

**Respuesta:** Para cargar datos de una fase a una tabla.

**Explicación:** `COPY INTO` carga datos desde archivos en un stage interno/externo hacia una tabla.

---

## 13/30 — SELECT COUNT ... LIMIT 10
**Pregunta:** ¿Qué se devolverá con `SELECT count FROM my_table LIMIT 10;`?

**Respuesta:** Un conjunto no determinante de 10 valores en la columna count.

**Explicación:** Sin `ORDER BY`, las filas devueltas no tienen un orden definido, por lo que el resultado es no determinista.

---

## 14/30 — Características de esquemas (Elegir DOS)
**Pregunta:** ¿Cuáles son características de los esquemas en Snowflake?

**Respuesta:**
1. Un esquema está contenido en una base de datos.
2. Los esquemas se usan para organizar objetos de bases de datos.

**Explicación:** Los esquemas son mutables, no contienen almacenes virtuales, y están disponibles para múltiples roles según los privilegios otorgados.

---

## 15/30 — Snowflake Cortex AI
**Pregunta:** ¿Qué tarea se puede realizar mediante Snowflake Cortex AI?

**Respuesta:** Extraer texto a partir de datos no estructurados.

**Explicación:** Snowflake Cortex AI incluye funciones como `PARSE_DOCUMENT` y `COMPLETE` para procesar y extraer información de datos no estructurados.

---

## 16/30 — Time Travel parameter
**Pregunta:** ¿Qué parámetro define por cuánto tiempo se puede usar Time Travel?

**Respuesta:** DATA_RETENTION_TIME_IN_DAYS.

**Explicación:** Este parámetro (a nivel de objeto o cuenta) define los días de retención para Time Travel.

---

## 17/30 — Objetos para COPY INTO (Elegir TRES)
**Pregunta:** ¿Qué objetos son necesarios para usar COPY INTO?

**Respuesta:**
1. Una fase
2. Una tabla
3. Un almacén virtual

**Explicación:** COPY INTO carga datos desde un **stage** hacia una **tabla**, y necesita un **warehouse** para ejecutar la consulta. Microparticiones son internas, data sharing y vistas no son necesarios.

---

## 18/30 — Lenguaje de cómputo en interfaces (Elegir DOS)
**Pregunta:** ¿Qué debe considerarse sobre el lenguaje de cómputo en interfaces de Snowflake?

**Respuesta:**
1. Las celdas de Notebook se pueden escribir en SQL.
2. Las celdas de Notebook se pueden escribir en Python.

**Explicación:** Los Notebooks soportan celdas SQL, Python, y otros lenguajes. Las hojas de trabajo (worksheets) también soportan Python y SQL.

---

## 19/30 — Historial de consultas
**Pregunta:** ¿Cómo se puede usar Snowsight para identificar consultas ejecutadas previamente?

**Respuesta:** Revisar la página del historial de consultas.

**Explicación:** Snowsight tiene una página *Query History* que muestra todas las consultas ejecutadas.

---

## 20/30 — Datos no estructurados
**Pregunta:** ¿En dónde se almacenan los datos no estructurados en Snowflake?

**Respuesta:** En fases internas o externas.

**Explicación:** Snowflake almacena datos no estructurados (PDFs, imágenes, etc.) en stages internos o externos, no en tablas directamente.

---

## 21/30 — Acceso a objetos
**Pregunta:** ¿Cuál es la manera recomendada de proporcionar acceso a un objeto a un rol?

**Respuesta:** Otorgar privilegios al rol.

**Explicación:** Se usa `GRANT <privilege> ON <object> TO ROLE <role>`.

---

## 22/30 — Nivel de Procesamiento de la Consulta
**Pregunta:** ¿Qué parámetro se configura en el nivel de Procesamiento de la Consulta?

**Respuesta:** El dimensionamiento de almacenes virtuales.

**Explicación:** El tamaño del warehouse (X-Small, Small, Medium, etc.) es una configuración del nivel de cómputo/procesamiento.

---

## 23/30 — Rol definido por el sistema
**Pregunta:** ¿Cuál es un rol definido por el sistema en Snowflake?

**Respuesta:** USERADMIN.

**Explicación:** USERADMIN es un rol predefinido del sistema. SNOWFLAKE_ADMIN, DATA_ENGINEER y SNOWFLAKE_DBA no son roles de sistema estándar.

---

## 24/30 — FLATTEN
**Pregunta:** ¿Qué columna se devuelve cuando se ejecuta la función de tabla FLATTEN?

**Respuesta:** VALUE.

**Explicación:** `FLATTEN` descompone datos semiestructurados y expone columnas como `VALUE`, `KEY`, `INDEX`, etc. `VALUE` contiene el valor real.

---

## 25/30 — PARSE_DOCUMENT
**Pregunta:** ¿Cuál es el fin PRINCIPAL de usar la función PARSE_DOCUMENT en Snowflake?

**Respuesta:** Extraer texto de archivos PDF.

**Explicación:** `PARSE_DOCUMENT` procesa archivos PDF, Word, PowerPoint en stages y extrae su contenido de texto.

---

## 26/30 — Acciones en base de datos desde Snowsight (Elegir DOS)
**Pregunta:** ¿Qué acciones se pueden realizar en una base de datos mediante el explorador de objetos?

**Respuesta:**
1. Cambiarle el nombre (Edit → rename)
2. Eliminarla (Drop)

**Explicación:** Desde Snowsight se puede cambiar el nombre y eliminar bases de datos. Mover, desconectar y cifrar no son acciones disponibles en el explorador.

---

## 27/30 — Nivel de Servicios en la Nube
**Pregunta:** ¿Qué se crea en el nivel de Servicios en la Nube de la arquitectura de Snowflake?

**Respuesta:** Metadatos.

**Explicación:** La capa de Cloud Services gestiona autenticación, metadatos, optimización de consultas, etc. Microparticiones están en la capa de almacenamiento, warehouses en la de cómputo.

---

## 28/30 — Formatos de datos semiestructurados (Elegir TRES)
**Pregunta:** ¿Cuáles formatos de datos semiestructurados admite Snowflake?

**Respuesta:** ORC, Avro, JSON.

**Explicación:** Snowflake soporta los formatos semiestructurados JSON, Avro, ORC, Parquet, XML, y otros. YAML y HTML no son formatos nativos; VCF es genómico.

---

## 29/30 — Variable de Python en celda SQL
**Pregunta:** ¿Qué sintaxis permite usar una variable de Python `myvar` en una celda SQL dentro de un Snowflake Notebook?

**Respuesta:** `{{myvar}}`

**Explicación:** En Snowflake Notebooks, las variables de Python se referencian en celdas SQL con la sintaxis de doble llave `{{variable}}`.

---

## 30/30 — SELECT *
**Pregunta:** ¿Para qué se usa la instrucción SQL SELECT * en Snowflake?

**Respuesta:** Para seleccionar todas las columnas de una tabla.

**Explicación:** `SELECT *` devuelve todas las columnas (y todas las filas que cumplan la condición).
