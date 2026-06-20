1. Creación y gestión de objetos de bases de datos
00:00 - 00:15
Bienvenido al Capítulo 2. En el último capítulo, cubrimos cómo Snowflake organiza los objetos en una jerarquía. Ahora vamos a ponernos manos a la obra — creando bases de datos y esquemas, ejecutando consultas y entendiendo cómo Snowflake gestiona el acceso a todo ello.

2. Creación de una base de datos y un esquema
00:15 - 00:57
Crear una base de datos en Snowflake es una sola línea de SQL. Ejecuta la declaración: `CREATE DATABASE` seguida del nombre de la base de datos. De manera similar, para crear un esquema, ejecuta `CREATE SCHEMA` y lo califica con el nombre de la base de datos, como en `CREATE SCHEMA snowy_peak_db.raw`, o proporciona solo el nombre del esquema — en ese caso, el esquema se crea en la base de datos de su contexto actual. Una vez creados, ambos aparecen inmediatamente en el explorador de objetos en Snowsight. A partir de aquí, el siguiente paso es decirle a Snowflake dónde quieres trabajar, y ahí es donde entra en juego el contexto.

3. Contexto de configuración
00:57 - 01:37
Antes de ejecutar cualquier consulta, recuerde configurar su contexto como lo explicamos en el último video. Estas cuatro líneas importan: rol, almacén, base de datos y esquema. Si establece solo una parte de la ruta, un `USE SCHEMA my_db.my_schema` completamente calificado (o un solo `USE SCHEMA` después de `USE DATABASE`), pero la parte importante es que la base de datos y el esquema sean inequívocos antes de ejecutarlos. Omita el almacén y recibirá un error (por ejemplo, "No hay ningún almacén activo seleccionado"). La solución es siempre la misma: configure su almacén y luego vuelva a ejecutarlo.

4. Consultando sus datos
01:37 - 02:16
Una vez configurado su contexto, la consulta funciona como cabría esperar. Una adición específica de Snowflake que vale la pena conocer es `EXCLUDE`. En lugar de enumerar todas las columnas que desea, selecciona todas las columnas y excluye las pocas que no necesita. Esto suele ser más fácil que una lista de selección larga para tablas anchas. `LIMIT` limita la cantidad de filas devueltas, lo cual es un buen hábito al explorar, pero no garantiza un escaneo más económico por sí solo; es posible que Snowflake aún necesite leer microparticiones relevantes según la consulta. Úselo junto con una lista de columnas sensata para explorar.

5. Entendiendo tus tablas
02:16 - 02:36
Cada base de datos de Snowflake viene con un esquema integrado llamado INFORMATION_SCHEMA. Es un conjunto de vistas de solo lectura que le brinda metadatos sobre todo lo que hay en su base de datos. Si le entregan una nueva base de datos y desea comprender qué contiene antes de escribir una única consulta comercial, este es su punto de partida.

6. Comprender sus columnas
02:36 - 03:03
INFORMATION_SCHEMA.COLUMNS profundiza una capa más — brindándole la estructura de una tabla específica. Nombres de columnas, tipos de datos, si se permiten valores nulos. Esto es útil cuando estás uniendo tablas y necesitas confirmar que los tipos coinciden, o cuando estás construyendo una canalización y necesitas saber qué campos pueden estar vacíos. Entre TABLAS y COLUMNAS, puedes comprender la estructura de una base de datos sin abrir una sola tabla directamente.

7. RBAC: Control de acceso basado en roles
03:03 - 03:38
El control de acceso en Snowflake sigue un modelo basado en roles: RBAC o control de acceso basado en roles. Cada objeto tiene un propietario: cualquier rol que lo haya creado. Los privilegios comunes incluyen `SELECT` para leer datos, `INSERT`, `UPDATE` y `DELETE` para escribirlos, y `USAGE` para acceder a una base de datos para poder usar objetos dentro de ella, un esquema o usar un almacén. Eliminar o alterar la estructura del objeto normalmente requiere privilegios de "PROPIEDAD" o DDL equivalentes.

8. RBAC: Concesión de privilegios en la práctica
03:38 - 04:18
Se requiere `USAGE` en la base de datos para que un rol trabaje con objetos en esa base de datos: sin él, es posible que no pueda consultar tablas incluso con `USAGE` en el esquema y `SELECT` en la tabla. En el ejemplo, primero otorgamos `USAGE` en la base de datos, luego el esquema y luego `SELECT` en la tabla. Los usuarios no obtienen privilegios directamente: se les asignan roles y el rol conlleva los privilegios. El principio del mínimo privilegio es la regla rectora. Por ejemplo, un analista que sólo lee datos no debería obtener permiso DDL en objetos de producción.