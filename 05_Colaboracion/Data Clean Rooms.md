1. Salas de limpieza de datos
00:00 - 00:00
El intercambio seguro de datos brinda al consumidor acceso de lectura directa a los datos de un proveedor. Pero a veces compartir datos sin procesar —incluso de sólo lectura— es demasiado. Es posible que dos empresas quieran colaborar en sus datos sin que ninguna de las partes vea los registros sin procesar de la otra. Ése es el problema que resuelve Data Clean Rooms.

2. Colaboración sin exposición
00:00 - 00:00
Claro quiere realizar una campaña de marketing conjunta con RetailCo. La pregunta es simple: ¿cuántos clientes aparecen en ambos conjuntos de datos? Esa respuesta les diría si vale la pena presentar una oferta conjunta. Pero Claro no puede compartir su lista de clientes con RetailCo, y RetailCo no puede compartir la suya con Claro — ambas listas contienen datos personales y financieros confidenciales. El intercambio de datos estándar no ayuda: daría a cada parte visibilidad de los registros sin procesar de la otra. Una sala limpia está diseñada exactamente para esto.

3. ¿Qué es una sala limpia de datos?
00:00 - 00:00
Una sala limpia de datos de Snowflake es un entorno seguro, creado sobre el marco de aplicaciones nativas, donde dos partes pueden colaborar en sus datos sin que ninguna de las partes vea los registros sin procesar de la otra. Cada parte aporta sus datos. Dentro de la sala limpia, las consultas aprobadas se ejecutan con los datos combinados. Sólo el resultado -un agregado o un recuento- vuelve a salir. Los discos sin procesar nunca salen de la sala limpia.

1 https://www.snowflake.com/en/product/features/data-clean-rooms/
4. ¿cómo funcionan las habitaciones limpias de Snowflake?
00:00 - 00:00
Ambas partes aportan sus datos. Los registros de clientes de Claro y los registros de clientes de RetailCo ingresan al entorno seguro. Una consulta aprobada se ejecuta dentro de — en este caso, una unión en un identificador de cliente hash para contar la superposición. El resultado es un solo número. Los discos sin procesar nunca salen de la sala limpia. Ninguna de las partes puede inspeccionar lo que aportó la otra. La sala limpia impone este límite a través de la lógica de consulta integrada en la aplicación nativa.

5. Funciones del proveedor y colaborador
00:00 - 00:00
Las habitaciones limpias tienen dos funciones. El proveedor — Claro — crea y configura la sala limpia: define qué consultas están permitidas, qué datos se pueden unir y qué resultados se pueden devolver. El colaborador — RetailCo — se une a la sala limpia, aporta sus datos y ejecuta las consultas aprobadas. El colaborador no puede modificar la lógica de la consulta ni cambiar las reglas de acceso. Esa asimetría es intencional: el proveedor mantiene el control sobre el límite de privacidad en todo momento. Esto es lo que hace que las salas blancas sean adecuadas para industrias reguladas donde una de las partes debe mantener el control total de cómo se desarrolla la colaboración.

6. Salas limpias versus intercambio seguro de datos
00:00 - 00:00
La distinción se reduce a una pregunta: ¿la otra parte necesita ver sus datos sin procesar o simplemente necesita la respuesta? El intercambio seguro de datos brinda al consumidor acceso directo para consultar, filtrar y explorar. Una sala limpia no brinda a ninguna de las partes acceso a los datos sin procesar de la otra, solo el resultado de una consulta aprobada conjuntamente. Los casos de uso comunes de salas blancas incluyen análisis de superposición de audiencias, medición conjunta de campañas y consorcios de detección de fraude donde múltiples instituciones comparten señales sin exponer sus registros subyacentes.

7. ¡Vamos a practicar!
00:00 - 00:00
Ahora ponga a prueba su comprensión de las habitaciones limpias versus el uso compartido seguro. Vamos a practicar.