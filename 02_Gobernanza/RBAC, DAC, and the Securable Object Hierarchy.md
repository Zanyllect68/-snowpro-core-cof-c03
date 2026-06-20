1. RBAC, DAC y la jerarquía de objetos asegurables
00:00 - 00:20
Hola y bienvenido a Snowflake Management, Governance and Collaboration. Este es nuestro segundo recorrido en la pista SnowPro Core. En este video, analizamos cómo Snowflake controla quién puede acceder a qué —, comenzando con el control de acceso basado en roles, el control de acceso discrecional y la jerarquía de objetos asegurables.

2. Presentamos a Claro
00:20 - 00:30
A lo largo de este curso trabajaremos con Claro, una aplicación global de creación de crédito que gestiona datos financieros confidenciales en múltiples regiones de Snowflake.

3. El problema del acceso
00:30 - 00:47
La cuenta de Claro contiene puntajes crediticios, historiales de pagos y registros financieros personales. Si no se administra, cualquier analista con un inicio de sesión podría consultarlo todo. Snowflake gestiona el acceso mediante una combinación de control de acceso basado en roles y control de acceso discrecional.

4. Los bloques de construcción
00:47 - 01:24
Cuatro términos sustentan el modelo de seguridad de Snowflake. Un privilegio es el permiso para actuar: SELECT te permite leer, INSERT te permite escribir, CREATE te permite construir. Un objeto es cualquier cosa sobre la que se pueda otorgar un privilegio: una tabla, un esquema, una base de datos o un almacén. Un rol es una entidad que tiene privilegios: puedes otorgar un rol a un usuario o a otro rol para construir una jerarquía. Un usuario es la persona o cuenta de servicio que se conecta a Snowflake y tiene roles.

5. Control de acceso basado en roles (RBAC): cómo funciona
01:24 - 01:48
El control de acceso basado en roles es la base para gestionar el acceso en Snowflake. Otorga privilegios sobre objetos a un rol y asigna el rol a los usuarios. SELECT on credit scores pasa al rol de analista, y el rol de analista pasa a María. Cuando un nuevo analista se une a Claro, le asignas el rol. Cuando se van, lo revocas. El rol se encarga de todo.

6. Implementación de RBAC
01:48 - 02:16
La primera declaración otorga a SELECT acceso en la tabla de puntajes crediticios de Claro al rol de analista. El segundo asigna ese papel a María. Estos son dos pasos distintos: se otorgan privilegios a los roles y se asignan roles a los usuarios. Tenga en cuenta que SELECCIONAR en la tabla por sí solo no es suficiente. El rol también necesita USO en el esquema y la base de datos que está encima de él. Cubriremos eso en un momento.

1 [Snowflake: Privilegios de control de acceso](https://docs.snowflake.com/en/user-guide/security-access-control-privileges)
7. Control de acceso discrecional (DAC)
02:16 - 02:43
Cada objeto en Snowflake tiene un dueño, siempre un rol, no una persona. El propietario decide quién más obtiene acceso. La propiedad se puede transferir utilizando GRANT PROPERTY. El control de acceso basado en roles define la estructura de roles. El DAC determina lo que cada rol controla dentro de él. Juntos te dan un modelo de acceso completo.

8. Transferencia de propiedad
02:43 - 03:07
La tabla de puntajes crediticios de Claro debe pasar del rol SYSADMIN al rol data_engineer. GRANT PROPERTY especifica la tabla y el rol que asume. El detalle crítico es REVOCAR LAS SUBVENCIONES ACTUALES al final. Sin ella, las concesiones del propietario anterior persisten junto con la nueva propiedad. Agregarlo hace que la transferencia sea limpia.

9. La jerarquía de objetos asegurables
03:07 - 03:29
Cada objeto en Snowflake vive en una jerarquía: organización, cuenta, bases de datos, esquemas y luego los objetos mismos. Para consultar una tabla, SELECT por sí solo no es suficiente, también necesita USAGE en el esquema y USAGE en la base de datos. Cada nivel debe concederse explícitamente. Si se pierde uno, la consulta falla.

10. Aplicando el USO en todos los niveles
03:29 - 03:50
Se requieren tres subvenciones para darle al rol de analista acceso a la tabla de puntajes crediticios de Claro: USAGE en la base de datos, USAGE en el esquema y SELECT en la tabla. El error más común es otorgar SELECT y olvidar las concesiones USAGE anteriores. La jerarquía exige que cada nivel de acceso sea deliberado.

11. Funciones definidas por el sistema
03:50 - 04:26
ACCOUNTADMIN se encuentra en la cima de la jerarquía de roles: hereda todo de todos los demás roles del sistema, así que resérvelo para la administración a nivel de cuenta, nunca para el trabajo diario. SYSADMIN crea bases de datos y almacenes. SECURITYADMIN posee políticas de red, políticas de enmascaramiento y gestión de roles, y también hereda los privilegios de USERADMIN, por lo que también puede crear y administrar usuarios. USERADMIN crea usuarios y asigna roles. PÚBLICO es el rol predeterminado que todo usuario obtiene automáticamente y nunca debe tener privilegios confidenciales.

1[ Snowflake: Descripción general del control de acceso](https://docs.snowflake.com/en/user-guide/security-access-control-overview)
12. ¡Vamos a practicar!
04:26 - 04:29
Pongamos a prueba tus conocimientos.

