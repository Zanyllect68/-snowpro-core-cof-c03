Aquí tienes la traducción al español de la transcripción:

**1. Formas de trabajar con Snowflake**
00:00 - 00:00
Snowflake no tiene una sola forma de acceso, tiene tres. Saber cuál elegir depende de lo que intentes hacer. En este video, conocerás las tres a través de un escenario que te resultará familiar una vez que trabajes con datos reales.

**2. Tres interfaces, tres trabajos diferentes**
00:00 - 00:00
Las tres formas principales de trabajar con Snowflake son Snowsight en el navegador, VS Code con la extensión de Snowflake en tu editor, y la CLI de Snowflake en la línea de comandos. Hemos resumido cada interfaz a grandes rasgos, pero profundizaremos más adelante en este video. Ahora, es lunes por la mañana en Snowy Peak. Un panel de control muestra números del viernes pasado. Algo no se ejecutó, o una consulta dio un error, o el *warehouse* no estaba disponible cuando debía estarlo. Necesitas entrar a Snowflake y averiguar qué sucedió. Y la herramienta adecuada para esta situación es Snowsight.

**3. Snowsight**
00:00 - 00:00
Snowsight es la interfaz de usuario del navegador, es donde la mayoría de las personas pasan la mayor parte de su tiempo. Cuando inicias sesión, deberías ver la pantalla de inicio. La interfaz está dividida en cuatro secciones clave: la sección 1 es la navegación, que se organiza en tres áreas: "Work with data" (Trabajar con datos), "Horizon Catalog" (Catálogo Horizon) y "Manage" (Administrar). La sección 2 actúa como una barra de búsqueda universal; la sección 3 incluye algunas acciones rápidas para que el usuario comience a trabajar con sus datos de inmediato. Finalmente, la sección 4 incluye todos tus proyectos y trabajos vistos recientemente para un acceso fácil. "Work with data" es donde pasarás la mayor parte de tu tiempo: Proyectos, Ingesta, Transformación, IA y ML, Monitoreo y Marketplace.

**4. Snowsight: Espacios de trabajo (*Workspaces*)**
00:00 - 00:00
Cuando navegas a Proyectos, tendrás varias opciones; la más utilizada es "Workspaces", que es el entorno de desarrollo predeterminado para Snowflake hoy en día. Un *workspace* es un editor privado basado en archivos donde puedes crear archivos SQL, Python y Notebooks, organizarlos en carpetas y trabajar en múltiples archivos uno al lado del otro. Si estás en una cuenta más antigua, es posible que veas *Worksheets* (hojas de trabajo); ese es el editor heredado. Ambos funcionan, pero los *Workspaces* son hacia donde se dirige Snowflake.

**5. Snowsight: Contexto**
00:00 - 00:00
En la parte superior de cualquier archivo abierto, verás los menús desplegables de contexto: rol, *warehouse*, base de datos y esquema. La base de datos y el esquema trabajan juntos; cuando eliges una base de datos, también eliges un esquema (o el predeterminado para esa base de datos). Configúralos antes de ejecutar cualquier cosa. Un contexto incorrecto es la razón número uno por la que una consulta falla cuando el SQL parece estar perfectamente bien. Por defecto, el rol y el *warehouse* pueden estar preseleccionados, pero asegúrate de establecer tu base de datos y esquema dentro de los menús desplegables de contexto o mediante SQL.

**6. Snowsight: Historial de consultas**
02:56 - 03:21
En Monitoreo, el Historial de Consultas te muestra todo lo que has ejecutado en tu cuenta: su estado, cuánto tiempo duró, quién la activó y qué *warehouse* utilizó. Si falta una consulta en la lista, abre los filtros en el Historial de Consultas. Opciones como "Don't consume query credits" (No consumir créditos de consulta) pueden ocultar algunas ejecuciones, así que ajusta los filtros y haz clic en "Apply" (Aplicar) para ver el panorama completo.

**7. Historial de consultas: Ejemplo simplificado**
03:21 - 03:39
Si estuvieras investigando un *pipeline* fallido, esta sería tu primera parada. Así es como descubres exactamente qué se rompió y cuándo. Esta es una de esas funciones que parecen ruido de fondo hasta que algo sale mal; entonces se convierte en una de las páginas más útiles en Snowflake.

**8. VS Code con la extensión de Snowflake**
03:39 - 04:13
Ahora probemos un escenario diferente: el ingeniero de datos de Snowy Peak está construyendo un modelo dbt y necesita verificar el SQL con datos en vivo. Podría abrir un navegador, pegar la consulta en una hoja de trabajo y volver a su editor, pero esa no es la forma más eficiente. En su lugar, debería ejecutarlo en VS Code con la extensión de Snowflake. Primero, instala la extensión de Snowflake desde el mercado (*marketplace*), autentícate una vez, y podrás ejecutar SQL directamente desde dentro de tu proyecto.

**9. Extensión de VS Code: Ejemplo simplificado**
04:13 - 04:25
No hay necesidad de cambiar de herramienta, la consulta reside junto al código al que pertenece. Esta es la herramienta adecuada cuando estás en un flujo de trabajo de desarrollo: escribir, probar e iterar, todo en un solo lugar.

**10. CLI de Snowflake**
04:25 - 04:41
Ahora, el escenario final. El *pipeline* de datos de Snowy Peak ejecuta un script de validación antes de cada despliegue: verificando recuentos de filas, valores nulos y rangos de fechas. Ningún humano hace clic en "ejecutar". Esto debe suceder automáticamente.

**11. CLI: Ejemplo simplificado**
04:41 - 05:05
Para eso sirve la CLI. La CLI de Snowflake reemplaza al antiguo SnowSQL. Te permite administrar objetos de Snowflake, desplegar aplicaciones, ejecutar consultas e interactuar con los servicios de Snowflake directamente desde tu terminal. Encaja en *pipelines* de CI, trabajos programados y, realmente, en cualquier cosa que se ejecute sin una persona interviniendo.

**12. ¡Practiquemos!**
05:05 - 05:10
Nos centraremos en la interfaz de Snowsight a lo largo de este curso. ¡Vamos a intentarlo!