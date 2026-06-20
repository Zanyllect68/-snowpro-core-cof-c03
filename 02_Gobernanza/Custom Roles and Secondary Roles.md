1. Roles personalizados y roles secundarios
00:00 - 00:16
En este video profundizaremos en cómo se diseñan los roles personalizados en la práctica: la diferencia entre roles funcionales y de acceso, cómo crearlos, cuándo usar roles de base de datos versus roles de cuenta y cómo funcionan los roles secundarios.

2. El problema de los escenarios de roles planos
00:16 - 00:41
Imagínese que Claro tiene tres analistas: Ana, Ben y Carlos. Cada uno necesita SELECT en las puntuaciones de crédito, USAGE en el esquema central y un puñado de otros privilegios. Administrado usuario por usuario, estás otorgando los mismos privilegios tres veces. Cuando se agrega una nueva tabla, se actualizan tres usuarios. Esto no escala. La solución es una jerarquía de roles deliberada.

3. Roles de acceso versus roles funcionales
00:41 - 01:22
Ambas capas utilizan el mismo objeto Snowflake, creado con CREATE ROLE; este es un patrón de diseño, no una característica diferente. No existe ninguna diferencia técnica entre un rol de acceso y un rol funcional en Snowflake; la distinción está en cómo se usan lógicamente. Los roles de acceso se encuentran en la parte inferior: cada uno tiene privilegios específicos sobre objetos específicos. CREDIT_READ mantiene SELECT en la tabla de puntajes crediticios de Claro. Los roles funcionales se ubican arriba y heredan de los roles de acceso. ANALYST podría heredar CREDIT_READ mientras que DATA_ENGINEER podría heredar tanto CREDIT_READ como PAYMENTS_WRITE.

1[ Snowflake: Alineación del acceso a objetos con funciones empresariales](https://docs.snowflake.com/en/user-guide/security-access-control-considerations#aligning-object-access-with-business-functions)
4. Cómo funciona
01:22 - 01:47
Los roles de acceso tienen privilegios específicos. Los roles funcionales heredan de uno o más roles de acceso. A los usuarios sólo se les asignan roles funcionales. Nunca tocan directamente los roles de acceso. Cuando Claro agrega una nueva tabla, actualiza CREDIT_READ una vez. Cada rol funcional que lo hereda, y cada usuario asignado a esos roles, obtiene el acceso automáticamente.

5. Construyendo la jerarquía en SQL
01:47 - 02:18
Primero, cree el rol de acceso y asígnele la cadena de privilegios completa: USO en la base de datos, USO en el esquema y SELECCIONAR en la tabla de puntajes crediticios. Los tres son obligatorios: si falta alguna de las subvenciones USAGE, el rol no puede llegar a la mesa. Luego cree el rol funcional ANALISTA y asígnele el rol CREDIT_READ usando GRANT ROLE. Un rol otorgado a otro construye la jerarquía. Por último, concede ANALISTA a Ana.

6. Roles de cuenta vs. roles de base de datos
02:18 - 02:44
Los roles de cuenta existen a nivel de cuenta y pueden abarcar cualquier base de datos o esquema. Los roles de la base de datos están limitados a una sola base de datos: solo pueden tener privilegios sobre objetos dentro de esa base de datos y no pueden asignarse directamente a los usuarios. En lugar de ello, se les concede un puesto de contabilidad. Esto permite a los propietarios de bases de datos administrar de forma independiente el acceso a sus propios objetos de base de datos sin necesidad de cambios de roles a nivel de cuenta.

7. Roles secundarios
02:44 - 03:27
Cada sesión tiene un rol principal, establecido con USE ROLE, que controla la propiedad del objeto y el contexto de creación. De forma predeterminada, los roles secundarios están configurados en TODOS: todos los demás roles que se le asignan están activos automáticamente junto con el principal. Los administradores pueden cambiar este valor predeterminado a nivel de cuenta. Si necesita un subconjunto específico, USE ROLES SECUNDARIOS seguidos del nombre del rol activa solo aquellos. UTILIZAR ROLES SECUNDARIOS NINGUNO restringe la sesión únicamente al rol principal. Un límite importante independientemente de la configuración del rol secundario: cualquier objeto que cree siempre será propiedad del rol principal.

1 [Snowflake BCR-1692: Cambio predeterminado de roles secundarios](https://docs.snowflake.com/en/release-notes/bcr-bundles/2024_08/bcr-1692)
8. Subvenciones futuras
03:27 - 03:50
Cuando se agrega una nueva tabla al esquema central de Claro, las subvenciones futuras significan que no es necesario recordar otorgar acceso manualmente. CONCEDER SELECCIONAR EN TABLAS FUTURAS en un esquema significa que cualquier tabla nueva creada allí hereda automáticamente la concesión, cerrando la brecha donde los nuevos objetos son visibles para los administradores pero invisibles para todos los demás.

9. ¡Vamos a practicar!
03:50 - 03:57
Gran trabajo, nos hemos sumergido más profundamente en roles personalizados y secundarios. Vamos a practicar.