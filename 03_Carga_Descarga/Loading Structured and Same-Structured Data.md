. Carga de datos estructurados y semiestructurados
00:00 - 00:10
En este video, cubriremos los métodos principales para obtener datos en Snowflake — cuándo usar cada uno, cómo funcionan las etapas y cómo manejar datos estructurados y semiestructurados.

2. El flujo de trabajo de carga
00:10 - 00:55
Antes de entrar en detalles, repasemos el flujo de trabajo típico para cargar datos en Snowflake. Sus archivos — CSV, JSON o cualquier otro formato: primero pasen a una etapa. Esa etapa es interna, administrada por Snowflake dentro de su cuenta, o externa, y apunta al almacenamiento en la nube que ya administra, como un depósito S3, GCS o Azure Blob. De cualquier manera, nada entra directamente en una mesa. Los archivos aterrizan en el escenario y luego ejecutas `COPY INTO` para cargarlos. Un objeto de formato de archivo (definido por separado) le dice al comando `COPY INTO` cómo analizar lo que está leyendo. Profundizaremos en cada paso en el resto del vídeo.

3. ¿Qué es un escenario?
00:55 - 01:37
Antes de poder utilizar COPY INTO, necesitas una etapa. Un escenario es una ubicación de almacenamiento temporal donde se encuentran sus archivos antes de cargarlos en una tabla. Hay dos tipos como acabamos de mencionar: Interno y Externo. Para crear una etapa interna, ejecuta `CREATE STAGE` seguido del nombre de la etapa. Para crear una etapa externa, también ejecuta `CREATE STAGE`, luego agrega una `URL` a tu almacenamiento en la nube y una integración de almacenamiento con parámetros relacionados para que Snowflake pueda acceder a esa ubicación de forma segura. De cualquier manera, el patrón es el mismo: los archivos aterrizan primero en la etapa y luego COPY INTO los mueve a la tabla.

4. Cargando datos en Snowflake
01:37 - 02:09
Hay tres formas principales de introducir datos en Snowflake. COPY INTO es el caballo de batalla — diseñado para carga masiva desde un escenario, maneja formatos estructurados y semiestructurados y escala bien. Este es el método que más utilizarás. INSERT funciona para agregar una pequeña cantidad de filas directamente sin preparar nada primero. Está bien para adiciones puntuales, pero no para conjuntos de datos grandes. El asistente de carga de la interfaz de usuario de Snowsight es la opción correcta para usuarios no técnicos o cargas únicas rápidas donde no es necesario escribir SQL.

5. Inspeccionar un escenario con LIST
02:09 - 02:40
Una vez creado tu escenario, inspecciona su contenido con LIST. El símbolo @ antes del nombre artístico le dice a Snowflake que estás haciendo referencia a un escenario, no a una mesa. Verás ese patrón durante las operaciones de carga y descarga. LIST devuelve todos los archivos en la etapa: nombre, tamaño y última marca de tiempo modificada. Es una verificación simple antes de ejecutar COPY INTO — confirmando que los archivos correctos están allí antes de comprometerse a cargarlos.

6. Carga de datos estructurados con COPY INTO
02:40 - 03:03
COPY INTO requiere tres cosas: la tabla de destino, el archivo de origen en el escenario y una definición de formato de archivo. El formato de archivo es de donde provienen la mayoría de los errores de carga — delimitador incorrecto, omisión de encabezado faltante o campos entre comillas mal manejados. La salida le indica si el archivo se cargó correctamente y cuántas filas se procesaron.

7. Carga y consulta de datos semiestructurados
03:03 - 03:41
Los datos semiestructurados como JSON se cargan en un tipo de columna especial de Snowflake llamado VARIANT. VARIANT puede contener cualquier estructura JSON sin necesidad de definir el esquema por adelantado; en cambio, Snowflake lo almacena tal cual. La carga funciona de la misma manera que CSV, solo que con un tipo de formato de archivo diferente. Al consultarlo es donde cambia la sintaxis, se utiliza la notación de dos puntos para navegar por la estructura JSON y luego se convierte el valor al tipo que se necesita. Al principio parece desconocido, pero es consistente: — dos puntos para navegar, dos puntos dobles para lanzar.

8. Cargando con la interfaz de usuario
03:41 - 04:08
Para cargas únicas o situaciones en las que SQL no es práctico, Snowsight tiene un asistente de carga incorporado. Lo encontrarás en el menú de acciones rápidas de la pantalla de inicio: Cargar archivos locales. Seleccione su tabla, cargue su archivo, configure las opciones de formato — no se requiere SQL. No es la herramienta adecuada para los procesos de producción, pero es realmente útil para obtener datos rápidamente durante la exploración o cuando una parte interesada no técnica necesita cargar un archivo por sí misma.

9. ¡Vamos a practicar!
04:08 - 04:12
¡Es hora de poner a prueba tus conocimientos!