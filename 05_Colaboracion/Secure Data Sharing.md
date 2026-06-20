1. Intercambio seguro de datos
00:00 - 00:23
En este capítulo pasamos de gobernar los datos dentro de la propia cuenta de Claro a compartirlos con el mundo exterior — de forma segura y deliberada. Este vídeo cubre el modelo seguro de intercambio de datos de Snowflake: cómo se comparten los datos entre cuentas sin que nunca se copien, quiénes son los jugadores y cómo manejar a los socios que no tienen su propia cuenta de Snowflake.

2. Problema con el intercambio de datos tradicional
00:23 - 00:55
Claro quiere compartir datos agregados de riesgo crediticio con un banco asociado. El enfoque tradicional: extraer los datos, transformarlos, transferirlos a través de SFTP o una API y luego hacer que el socio los cargue en su sistema. Cuando aterriza, ya está desactualizado. Es una copia, las copias se desvían, necesitan actualización, reconciliación y seguridad en cada paso. El modelo compartido de Snowflake elimina todo eso.

3. Cómo funciona el uso compartido de copos de nieve
00:55 - 01:27
El uso compartido de Snowflake brinda a una cuenta de consumidor acceso de lectura directa a los objetos en la cuenta del proveedor — sin copiar ningún dato. El almacenamiento subyacente es compartido. Cuando el banco asociado consulta la base de datos compartida, lee los datos de Claro en tiempo real. En el momento en que Claro actualiza un registro, el socio ve la actualización en su próxima consulta. Sin canalizaciones, sin copias obsoletas y sin riesgo de transferencia. Todos los datos viven en un solo lugar.

4. Creando la acción
01:27 - 02:04
Crear un recurso compartido implica tres pasos. Primero, cree el objeto compartido en sí. En segundo lugar, otorgue los objetos que desea exponer: USO en la base de datos y el esquema, SELECCIONAR en la tabla específica. Se aplica la misma jerarquía de USO del Capítulo 1. En tercer lugar, otorgar la acción a la cuenta del consumidor especificando su identificador de cuenta. A partir de ese momento, el banco socio podrá ver la acción. Claro controla exactamente lo que contiene y puede agregar o eliminar objetos y cuentas en cualquier momento.

5. Montar una acción
02:04 - 02:35
Del lado del consumidor, la configuración es un solo paso: CREAR BASE DE DATOS DESDE COMPARTIR. El banco asociado especifica la referencia de la acción y le asigna un nombre de base de datos local. A partir de ese momento lo consultan como cualquier otra base de datos. SELECT parece idéntico a cualquier otra consulta. Pero nada se ha movido. Cada consulta lee desde el almacenamiento de Claro en tiempo real. El consumidor puede consultar pero no puede escribir, clonar ni volver a compartir los datos.

6. Cuentas de lectores
02:35 - 03:12
No todos los socios tienen una cuenta Snowflake — ahí es donde entran en juego las cuentas de lectores. Claro crea y administra la cuenta del lector en nombre del socio: una cuenta Snowflake liviana con un propósito: consultar el recurso compartido. El socio obtiene credenciales y puede consultar los datos compartidos inmediatamente. La contrapartida: con una cuenta de consumidor estándar, el consumidor paga por su propio cómputo. Con una cuenta de lector, Claro paga el cómputo. Las cuentas de lectores también se limitan únicamente a datos compartidos.

7. Vistas seguras al compartir
03:12 - 03:45
De forma predeterminada, los recursos compartidos de Snowflake se configuran con SECURE_OBJECTS_ONLY establecido en verdadero, lo que significa que solo se pueden compartir vistas seguras. Una vista segura permite al consumidor consultar los resultados, pero oculta la definición de la vista por completo, por lo que el banco asociado no puede inspeccionar el SQL subyacente ni ver qué columnas se excluyeron. Puede configurar SECURE_OBJECTS_ONLY en falso para permitir compartir vistas estándar, pero Snowflake recomienda encarecidamente no hacerlo cuando las tablas subyacentes contengan datos confidenciales.

1 https://docs.snowflake.com/en/user-guide/data-sharing-secure-views
8. ¡Vamos a practicar!
03:45 - 03:51
Ahora es tu turno de configurar una acción y montarla como consumidor. Vamos a practicar.