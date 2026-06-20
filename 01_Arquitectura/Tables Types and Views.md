1. Tipos de tablas y vistas
00:00 - 00:00
Ahora que sabe cómo funcionan las microparticiones, repasaremos los tipos de tablas y vistas de Snowflake en un orden lógico.

2. Tipos de tablas y vistas
00:00 - 00:00
Comenzamos con tablas permanentes, transitorias y temporales (donde los viajes en el tiempo y las tablas a prueba de fallos difieren), luego tipos de tablas especializadas, luego vistas estándar y materializadas y, finalmente, vistas seguras para compartir. Un capítulo posterior profundiza en la recuperación operativa con viajes en el tiempo y clonación; aquí solo necesitamos los nombres de las características para explicar cada objeto.

3. Permanente, Transitorio y Temporal
00:00 - 00:00
Cada tabla que se crea en Snowflake tiene un tipo, de los cuales hay tres: permanente, transitoria y temporal. Piense en los tres tipos de tablas como una escala móvil entre protección y costo. El valor predeterminado es permanente. En un extremo, las tablas permanentes le brindan la pila completa: Time Travel plus Fail-safe, una ventana de recuperación de 7 días administrada por Snowflake. En la Enterprise Edition obtienes hasta 90 días de viaje en el tiempo; en Standard, 1 día. Las tablas temporales se encuentran en el otro extremo: solo existen durante la duración de tu sesión y desaparecen cuando cierras sesión. Las tablas transitorias aterrizan en el medio, manteniendo hasta un día de viaje en el tiempo pero abandonando por completo Fail-safe. Cuanto más protección necesites, más almacenamiento te costará. Las mesas transitorias y temporales no tienen protección contra fallos, y es exactamente por eso que son más baratas de almacenar.

4. Permanente, Transitorio y Temporal
00:00 - 00:00
Si está creando tablas de preparación o resultados intermedios en los que no necesita protección a largo plazo, transient es el valor predeterminado correcto. Más allá de permanente, transitorio y temporal, Snowflake tiene cuatro tipos de mesas más especializadas.

5. Dinámico, externo e híbrido
00:00 - 00:00
Las tablas dinámicas automatizan el trabajo de actualización que de otro modo realizarías en un trabajo programado. Escribes una consulta, estableces un retraso objetivo que es qué tan atrás de los datos de origen estás dispuesto a estar y Snowflake mantiene el resultado actualizado. Se aplican tanto el viaje en el tiempo como el sistema a prueba de fallos. Las tablas externas son el otro extremo. Los datos permanecen en el almacenamiento en la nube y nunca se cargan en Snowflake. Lo consultas en el lugar y es de solo lectura. Sin viajes en el tiempo, sin medidas de seguridad.

6. Dinámico, externo e híbrido
00:00 - 00:00
Las tablas híbridas están diseñadas para cargas de trabajo que combinan escrituras a nivel de fila de alta frecuencia con lecturas analíticas de una aplicación operativa que también necesita ejecutar informes. Si bien se admite el viaje en el tiempo, no se admite el método a prueba de fallos.

7. Apache Iceberg™
02:32 - 02:57
Apache Iceberg™ es un formato de tabla abierta, un estándar que permite que múltiples motores de procesamiento como Spark, Trino y Snowflake trabajen con los mismos datos sin copiarlos. Snowflake te ofrece dos variantes. Con un catálogo administrado por Snowflake, Snowflake maneja los metadatos y Time Travel funciona como cabría esperar, pero no existe un sistema a prueba de fallos.

8. Apache Iceberg™
02:57 - 03:24
With an externally-managed catalog, the catalog lives outside Snowflake — in AWS Glue, for example — but the table itself can be read from and written to from Snowflake's side. Time Travel is still supported in both cases but Fail-safe is not. Reach for Iceberg when the data lake is your source of truth and you need multiple engines working against the same tables without duplication.

9. Time Travel and Fail-safe (with table types)
03:24 - 03:45
Time Travel lets you query or recover data as it existed within the retention window. Fail-safe is a separate, short safety net after that window. Which features apply depends on the table type and edition, which is why we introduce the names here and return to operational examples in the data-protection chapter.

10. Standard View and Materialized View
03:45 - 04:24
Snowflake has two types of views: standard and materialized. Both can be created as secure: a property on the view, not a third “kind” in the same sense. A standard view is a stored query: each use runs a fresh query against the base tables, with no extra persistent result storage. A materialized view stores precomputed results and refreshes as the data changes. Her we trade storage and serverless maintenance for faster reads when the same expensive pattern runs often and data changes slowly.

11. Secure View
04:24 - 05:03
Se puede aplicar una vista segura a una vista estándar o materializada. El cambio importante es que con una vista segura la definición de la vista no queda expuesta al consumidor y su lógica de negocio permanece privada. Cuando el equipo de Snowy Peak comparte datos con un socio de seguros, expone una vista de puntuación de riesgo. El socio ve las puntuaciones, no el cálculo detrás de ellas. Las vistas seguras son el mecanismo que hace que compartir externamente sea seguro sin brindarles a los socios una ventana a su lógica. Hay un pequeño costo de rendimiento, por lo que solo utilícelos cuando el beneficio de privacidad lo justifique.

12. ¡Vamos a practicar!
05:03 - 05:07
Es hora de poner en práctica lo que has aprendido sobre las opiniones.