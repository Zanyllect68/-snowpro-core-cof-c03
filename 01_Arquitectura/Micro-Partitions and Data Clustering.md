. Microparticiones y agrupamiento de datos
00:00 - 00:00
Bienvenido al Capítulo 3. En el último vídeo, cubrimos las diferentes formas en que puedes cargar datos en Snowflake. Ahora es el momento de echar un vistazo debajo del capó a lo que realmente sucede cuando Snowflake almacena esos datos y por qué es importante para el rendimiento de sus consultas.

2. Consultar una tabla grande
00:00 - 00:00
Empecemos con un ejemplo. A fin de mes, el equipo de Snowy Peak está ejecutando una consulta para extraer las suscripciones del último mes para un informe comercial. Esta tabla contiene tres años de datos de eventos, con más de mil millones de filas. Cada vez que se ejecuta, la consulta tiene que decidir cuántos datos necesito leer de esta tabla? Las bases de datos tradicionales utilizan índices, pero Snowflake no. ¿Qué método aplican?

3. Microparticiones
00:00 - 00:00
Ingrese microparticiones. Cuando los datos se cargan en Snowflake, se dividen automáticamente en microparticiones, que son fragmentos de almacenamiento en disco del orden de 50 a 500 MB de datos sin comprimir. El tamaño real en el disco está comprimido y es más pequeño. Dentro de cada partición, las columnas se almacenan y comprimen por separado. Este diseño de columnas es una de las principales razones por las que las consultas de Snowflake pueden ser rápidas en tablas grandes porque solo lee las columnas que una consulta realmente necesita. Lo más importante es que todo esto sucede automáticamente en segundo plano.

4. Metadatos
00:00 - 00:00
Para cada micropartición que crea Snowflake, almacena metadatos que incluyen el valor mínimo y máximo de cada columna, el recuento de filas, los recuentos nulos y los recuentos de valores distintos. Estos metadatos se almacenan en la capa de servicios en la nube y se mantienen automáticamente a medida que se cargan y actualizan los datos.

5. Poda de particiones
00:00 - 00:00
Ahora veamos un ejemplo, digamos que queremos filtrar una tabla de ventas en función del mes de mayo.

6. Poda de particiones
00:00 - 00:00
Snowflake verifica los valores de fecha mínima y máxima almacenados para cada partición, y se omitirá cualquier partición donde el rango de fechas no incluya los datos de mayo. Este motor nunca toca esas filas, este concepto se llama poda de particiones.

7. Agrupamiento
00:00 - 00:00
La poda solo funciona bien cuando la columna en la que intentas filtrar está bien agrupada, lo que significa que las filas con valores similares se agrupan en las mismas microparticiones. Si los eventos de Snowy Peak se cargan en orden de fecha, las consultas basadas en fechas se podarán bien porque el orden de clasificación natural de los datos hace el trabajo. Sin embargo, si filtra por región o plan de suscripción y esos valores están dispersos en las particiones independientemente del orden de carga, la poda puede no ayudar tanto. Puede definir una clave de agrupamiento para que Snowflake organice microparticiones alrededor de esa columna para futuros pases de mantenimiento.

8. Clave de agrupamiento: cuándo utilizarla
00:00 - 00:00
Una clave de agrupamiento tiene sentido cuando tres cosas son ciertas: la tabla es lo suficientemente grande como para que la poda realmente importe, piense en cientos de gigabytes; estás filtrando constantemente en la misma columna; y esa columna está mal agrupada, lo que significa que la poda no funciona para ella.

9. Clave de agrupamiento: cardinalidad y costo
00:00 - 00:00
La cardinalidad también importa aquí. Una columna con muy pocos valores distintos, como una bandera booleana, no creará límites de partición significativos, por lo que no es un buen candidato. Hay una cosa más que vale la pena saber: Snowflake se vuelve a agrupar automáticamente con el tiempo a medida que llegan nuevos datos, utilizando su propia computación sin servidor en lugar de su almacén virtual. Eso es útil, pero aumenta tu factura. Por lo tanto, la agrupación de claves debe ser una decisión deliberada y consciente de los costos. No es algo que apliques por defecto.

10. ¡Vamos a practicar!
00:00 - 00:00
¡pongamos a prueba tus conocimientos sobre microparticiones y agrupación de datos!