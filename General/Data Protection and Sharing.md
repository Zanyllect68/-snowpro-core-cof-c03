1. Protección y compartición de datos
00:00 - 00:00
En este video cubrimos dos de las características más poderosas de Snowflake para el trabajo de datos de producción: viajes en el tiempo para recuperarse de errores y clonación sin copia para crear copias instantáneas de sus datos. También abordaremos cómo funciona el intercambio de datos en Snowflake.

2. Cuando algo sale mal
00:00 - 00:00
Un analista de Snowy Peak ejecuta un DELETE con la cláusula WHERE incorrecta. Han desaparecido ochocientas cuarenta y siete filas de suscripciones activas. En la mayoría de las bases de datos, se trata de un ticket de soporte y una restauración de la copia de seguridad de anoche, pero son horas de inactividad y datos potencialmente perdidos. Con Snowflake, es una solución rápida porque Snowflake conserva el estado de sus datos antes de cada cambio. Es automático sin configuración extra, solo necesitas configurar la ventana de tiempo. Esa ventana es algo que tocamos en videos anteriores, se llama Viaje en el Tiempo.

3. Viaje en el tiempo
00:00 - 00:00
Time Travel le permite consultar datos tal como existían en cualquier punto dentro de la ventana de retención. Usted establece esa ventana con el parámetro `DATA_RETENTION_TIME_IN_DAYS` a nivel de tabla, y también puede establecer valores predeterminados o anulaciones en el ámbito del esquema, la base de datos o la cuenta; gana el nivel más bajo. En la edición estándar, el caso común es una ventana de un día; en Enterprise y versiones superiores, a menudo se pueden extender hasta noventa días en objetos elegibles. Consulte la edición actual y las reglas del objeto en la documentación. Los viajes en el tiempo no se limitan a las consultas SELECT. Funciona con CREATE TABLE AS SELECT, operaciones CLONE y UNDROP, el comando que restaura un objeto eliminado. Acceso histórico a todo el ciclo de vida del objeto, no solo a las filas dentro de una tabla.

4. Historial de navegación: marca de tiempo y desplazamiento
00:00 - 00:00
`AT TIMESTAMP` te fija en un momento exacto. `AT OFFSET` o un intervalo con signo retrocede una duración conocida, por ejemplo, una hora.

5. Navegando por el historial: declaración y eliminación
00:00 - 00:00
`BEFORE(STATEMENT => '…')` y `AT BEFORE` vinculan la recuperación a una declaración específica utilizando su ID de consulta, usted regresa al estado de los datos inmediatamente antes de que se ejecute esa declaración. En Snowflake, `DROP` elimina un objeto, no significa "regresar en el tiempo" por sí solo. Si alguien dejó caer una mesa accidentalmente, use `UNDROP. Por ejemplo, `UNDROP TABLE t`, mientras el objeto aún se puede recuperar en la cuenta.

6. Fail-Safe
00:00 - 00:00
Más allá de la ventana de viaje en el tiempo, Snowflake retiene automáticamente sus datos durante siete días más en Fail-safe. Esto está activado de forma predeterminada — no hay nada que habilitar o configurar. No puedes consultarlo tú mismo durante ese período, pero si lo necesitas, Snowflake Support puede recuperarlo por usted. Esa recuperación está incluida en su cuenta — no hay ningún cargo de soporte adicional por ello. Lo que cuesta dinero es el almacenamiento en sí: los datos en Fail-safe todavía cuentan para su factura durante esos siete días. Es un último recurso, no un reemplazo para los viajes en el tiempo. Hay cuatro etapas por las que pasan tus datos en Snowflake. Vivir es lo que existe ahora mismo. Time Travel te permite retroceder a la historia hasta un día en la Edición Estándar, hasta noventa días en Enterprise y superiores. Más allá de eso,Fail-safe le da a Snowflake siete días más para recuperar datos en su nombre si es necesario. Después de eso, los datos desaparecen y son irrecuperables.

7. Clonación sin copia
00:00 - 00:00
La clonación sin copia crea una copia independiente de una tabla, esquema o base de datos con una sola línea de SQL. Ejecuta el comando CLONE explícitamente — esto no es algo que Snowflake haga automáticamente en segundo plano. En el momento de la creación, el clon comparte el almacenamiento subyacente con el original, por lo que ningún dato se duplica físicamente y es efectivamente instantáneo independientemente del tamaño de la tabla. El almacenamiento solo se carga cuando los dos comienzan a divergir — cuando escribes en uno y no en el otro. Y lo que es más importante, son totalmente independientes: los cambios en el clon nunca tocan el original, y los cambios en el original nunca afectan al clon. Para Snowy Peak, clonan la tabla de suscripciones antes de cada cambio de esquema de producción, con cero riesgos y cero esperas.

8. Mercado de copos de nieve
00:00 - 00:00
Por último, Snowflake Marketplace le permite incorporar conjuntos de datos externos, como datos meteorológicos, datos demográficos y fuentes financieras de proveedores externos, directamente dentro de su cuenta de Snowflake. Los datos compartidos aparecen como una base de datos sin necesidad de carga ni canalización ETL. Snowy Peak podría extraer datos meteorológicos históricos y unirlos directamente a la tabla avalanche_events. El intercambio privado de datos extiende esto al intercambio con cuentas específicas, lo que resulta útil para la colaboración controlada de datos con socios o equipos internos.

9. ¡Vamos a practicar!
00:00 - 00:00
Has visto cómo los viajes en el tiempo te permiten consultar y restaurar datos del pasado, y cómo la clonación te proporciona copias instantáneas y eficientes en almacenamiento. Pongamos esas habilidades a trabajar.