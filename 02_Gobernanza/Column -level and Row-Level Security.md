1. Seguridad a nivel de columna y de fila
00:00 - 00:00
El control de acceso a nivel de objeto es binario — un rol puede consultar una tabla o no. ¿Qué pasa cuando necesitas algo más matizado? Eso es lo que cubre este vídeo: seguridad a nivel de columna y a nivel de fila.

2. El problema del acceso a nivel de tabla
00:00 - 00:00
La tabla de usuarios de Claro contiene nombres, direcciones de correo electrónico, puntajes crediticios y banda crediticia. Cuando le otorgas a SELECT el rol de analista, ellos pueden verlo todo. Un analista que publica informes de campaña no necesita puntajes crediticios brutos. El control de acceso a nivel de tabla no puede hacer esa distinción — se necesita seguridad en un grano más fino.

3. ¿Qué es la seguridad a nivel de columna?
00:00 - 00:00
La seguridad a nivel de columna no elimina una columna de los resultados de la consulta. La columna sigue ahí — lo que cambia es el valor que aparece, dependiendo de quién pregunte. Un rol privilegiado implica un puntaje crediticio real. Un rol sin privilegios ve un valor enmascarado. Los datos subyacentes no han cambiado. El enmascaramiento ocurre en el momento de la consulta y se aplica sobre la marcha en función del rol de consulta. El mecanismo se llama enmascaramiento dinámico de datos.

4. Enmascaramiento dinámico de datos
00:00 - 00:00
El enmascaramiento dinámico de datos funciona adjuntando una política de enmascaramiento a una columna. La política es una función SQL que toma el valor de la columna como entrada y devuelve el valor real o una versión enmascarada, según la función de consulta. El rol de analista ve NULL donde deberían aparecer los puntajes crediticios. Sin embargo, el rol de administrador de crédito ve esos valores reales. La tabla y la consulta son idénticas — la política de enmascaramiento maneja el resto automáticamente.

5. Creación y aplicación de una política de enmascaramiento
00:00 - 00:00
La política de enmascaramiento se crea como una función: si la sesión de consulta incluye el rol CREDIT_ADMIN, devuelve el puntaje crediticio real; de lo contrario, devuelve un valor centinela. Aquí utilizamos IS_ROLE_IN_SESSION, que verifica todos los roles activos en la sesión, incluidos los roles heredados y secundarios. CURRENT_ROLE, por el contrario, solo devuelve el rol principal activo, por lo que un usuario que tenga CREDIT_ADMIN como rol secundario obtendría datos enmascarados si usara CURRENT_ROLE en su lugar. Una vez definida, la política se aplica a la columna con ALTER TABLE MODIFICAR COLUMNA. Cada consulta posterior se filtra a través de ella automáticamente.

1 https://docs.snowflake.com/en/sql-reference/sql/create-masking-policy#example-normal-masking-policy
6. Tokenización externa
00:00 - 00:00
Snowflake también admite la tokenización externa. En lugar de enmascarar valores en línea, Snowflake llama a una función externa que se conecta a un proveedor de tokenización de terceros. El proveedor reemplaza el valor confidencial con un token. Debido a que la tokenización ocurre fuera de Snowflake, el mismo token puede reconocerse en múltiples sistemas. Esto es útil para organizaciones que procesan datos en varias plataformas y necesitan identificadores tokenizados consistentes en todas partes.

1 https://docs.snowflake.com/en/user-guide/security-column-ext-token-use
7. ¿Qué es la seguridad a nivel de fila?
00:00 - 00:00
La seguridad a nivel de fila controla qué filas aparecen, no qué valores aparecen en las columnas. Claro tiene analistas en EEUU y UE. Ambos consultan la tabla de usuarios, pero cada uno solo debe ver a los usuarios de su región. La seguridad a nivel de fila hace que esto suceda automáticamente. El analista ejecuta un SELECT simple sin cláusula WHERE. Snowflake aplica un filtro de filas detrás de escena según el rol del analista. El mecanismo se llama Política de acceso a filas.

8. Cómo funcionan las políticas de acceso a filas
00:00 - 00:00
Cuando un analista consulta la tabla de usuarios, Snowflake pasa la consulta a través de la Política de acceso a filas adjunta a esa tabla. La política evalúa el rol de consulta — US_ANALYST — y aplica un filtro: solo se devuelven las filas donde la región es igual a US. Un analista de EU_ANALYST ejecutaría la misma consulta y solo vería las filas de la UE.

9. Creación y aplicación de una política de acceso a filas
00:00 - 00:00
La política de acceso a filas es una función que toma un valor de columna y devuelve un valor booleano: verdadero si la fila debe ser visible, falso si no. El bloque CASE utiliza IS_ROLE_IN_SESSION, por lo que se verifican los roles heredados y secundarios, no solo el principal. US_ANALYST ve filas de EE. UU., EU_ANALYST ve filas de la UE, cualquier otro rol no ve nada porque ELSE devuelve falso. La política se aplica con ALTER TABLE ADD ROW ACCESS POLICY, especificando con qué columna se evalúa la política.

10. Uso conjunto de políticas de enmascaramiento de datos y acceso a filas
00:00 - 00:00
Las políticas de enmascaramiento dinámico de datos y acceso a filas son independientes pero ambas pueden aplicarse a la misma tabla. Snowflake aplica primero la Política de acceso a filas, filtrando las filas que el rol no debería ver. Luego, el enmascaramiento dinámico de datos se aplica a las columnas dentro de las filas restantes. Es posible que un analista solo vea a los usuarios de su región y, dentro de esas filas, la columna de puntaje crediticio aún esté enmascarada.

11. ¡Vamos a practicar!
00:00 - 00:00
Ahora es su turno de aplicar políticas de enmascaramiento y políticas de acceso a filas. Vamos a practicar.