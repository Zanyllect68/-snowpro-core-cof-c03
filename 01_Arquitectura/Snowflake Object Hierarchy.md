1. Jerarquía de objetos Snowflake
00:00 - 00:00
Bienvenido de nuevo. Ahora veamos cómo Snowflake organiza todo lo que hay dentro. Comprender la jerarquía de objetos es una de esas cosas que hace que todo lo demás haga clic: consultas, control de acceso, carga de datos. Todo se remonta a esta estructura.

2. Comprender la jerarquía de objetos
00:00 - 00:00
Snowflake organiza todo en cinco niveles y la mejor manera de entenderlo es construirlo desde afuera hacia adentro. El nivel de organización es el contenedor más externo. La mayoría de los equipos no interactuarán con él directamente día a día, pero es donde se gestionan la replicación entre cuentas y la facturación centralizada. Puede agrupar varias cuentas de Snowflake. Esto es útil para empresas que gestionan varios entornos o regiones.

3. Comprender la jerarquía de objetos
00:00 - 00:00
Directamente debajo, la cuenta. Este es su entorno Snowflake: vinculado a un proveedor de nube específico, una región específica y una edición específica. Cuando alguien dice "nuestra cuenta de Snowflake", esto es lo que quiere decir. Todo lo que está debajo se encuentra dentro de este límite.

4. Comprender la jerarquía de objetos
00:00 - 00:00
Dentro de la cuenta viven seis tipos de objetos: usuarios, roles, bases de datos, almacenes virtuales, monitores de recursos e integraciones. Estos existen en todo su entorno: no dentro de una base de datos específica.

5. Comprender la jerarquía de objetos
00:00 - 00:00
Las bases de datos se encuentran dentro de la cuenta y actúan como contenedores lógicos. Dentro de cada base de datos, los esquemas organizan sus objetos. Una base de datos llamada ANALYTICS podría tener esquemas llamados RAW, STAGING y MARTS, cada uno de los cuales contiene tablas y vistas en una etapa diferente de transformación.

6. Comprender la jerarquía de objetos
00:00 - 00:00
Y en la parte inferior, los objetos mismos: tablas, vistas, UDF y más. Todo en Snowflake vive en algún lugar de esta jerarquía, y comprender a qué nivel pertenece un objeto es lo que hace que las consultas, los permisos y la carga de datos hagan clic.

7. Objetos a nivel de cuenta vs. objetos a nivel de base de datos
00:00 - 00:00
Recuerde, no todos los objetos se encuentran dentro de una base de datos. Algunos vivirán a nivel de cuenta, como usuarios, roles, almacenes e integraciones que existen en todo su entorno Snowflake, no dentro de ninguna base de datos específica. Los objetos a nivel de base de datos son aquellos con los que probablemente esté más familiarizado: tablas, vistas, etapas, UDF y procedimientos almacenados. La distinción es importante porque el control de acceso funciona de manera diferente dependiendo de dónde se encuentre un objeto. Un almacén se comparte entre bases de datos, mientras que una tabla pertenece exactamente a un esquema.

1 https://docs.snowflake.com/en/user-guide/security-access-control-overview
8. Contexto
00:00 - 00:00
Antes de ejecutar cualquier consulta en Snowflake, es necesario configurar cuatro cosas: su rol, su almacén, su base de datos y su esquema. Puede configurarlos usando declaraciones SQL USE: USE ROLE, USE WAREHOUSE, USE DATABASE y USE SCHEMA. En Snowy Peak, un ingeniero de datos establece su función en ANALYST, su almacén en COMPUTE_WH y su base de datos y esquema en la capa ANALYTICS. Todo lo que sigue se desarrolla en ese contexto Puede verificar lo que está configurado actualmente en cualquier momento utilizando las funciones de contexto: CURRENT_ROLE, CURRENT_WAREHOUSE, CURRENT_DATABASE y CURRENT_SCHEMA. Ejecútelos en un SELECT y verá exactamente en qué sesión está operando.

9. Variables de sesión
00:00 - 00:00
Más allá del contexto, hay dos herramientas más que viven a nivel de sesión. Las variables de sesión le permiten almacenar y reutilizar valores dentro de un script. Establezca uno con la función SET, por ejemplo, SET min_users = 100 y luego haga referencia a él en cualquier lugar de esa sesión usando el signo de dólar min_users.

1 https://docs.snowflake.com/en/sql-reference/sql/set
10. Jerarquía de parámetros: Parámetros de cuenta
00:00 - 00:00
Los parámetros se denominan configuraciones que controlan cómo se comporta Snowflake y se dividen en cuatro tipos, cada uno con su propia cadena de anulación. Los parámetros de la cuenta se encuentran en la parte superior y no se pueden anular. Lo que se aplica es lo que se establece a nivel de cuenta, cosas como PERIODIC_DATA_REKEYING.

1 https://docs.snowflake.com/en/sql-reference/parameters
11. Parámetros de sesión
00:00 - 00:00
Los parámetros de sesión funcionan de manera diferente. La cuenta establece un valor predeterminado, un administrador puede anularlo para un usuario específico y el usuario puede anularlo nuevamente dentro de su sesión activa. Gana el nivel más bajo en el que se establece el parámetro.

12. Parámetros del almacén virtual
00:00 - 00:00
Los parámetros del almacén virtual siguen una cadena más simple de dos niveles: cuenta predeterminada y luego anulada en el propio almacén. STATEMENT_TIMEOUT_IN_SECONDS es el clásico — es posible que desee un tiempo de espera más ajustado en el almacén de su panel de control que el que permite el valor predeterminado de la cuenta.

13. Parámetros de la tabla
00:00 - 00:00
Finalmente, los parámetros de la base de datos, el esquema y la tabla caen en cascada a través de la jerarquía de objetos. Establezca un valor predeterminado a nivel de cuenta, anúlelo en la base de datos, limítelo aún más en el esquema y anúlelo nuevamente en una tabla específica. DATA_RETENTION_TIME_IN_DAYS funciona de esta manera, su cuenta puede tener como valor predeterminado un día, pero sus tablas de facturación más importantes obtienen treinta. La regla para los cuatro tipos es la misma: se utilizará el nivel más bajo en el que se establece el parámetro y ese valor gana.

14. ¡Vamos a practicar!
00:00 - 00:00
Es hora de poner en práctica lo aprendido.