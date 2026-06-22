1. Tipos de datos SQL de Snowflake
00:00 - 00:11
¡Hola de nuevo! Ahora vamos a ver algunos tipos de datos comunes y específicos de Snowflake SQL y PostgreSQL, y cómo convertir datos de un tipo a otro.

2. Tipos de datos frecuentes
00:11 - 00:24
Hay muchos tipos de datos que son comunes a ambas variantes de SQL; veamos algunos de ellos. Los tipos de datos de cadena incluyen `VARCHAR`,`CHAR` , y `TEXT`.

3. Tipos de datos frecuentes
00:24 - 00:27
Los números enteros se pueden guardar como `INTEGER`s.

4. Tipos de datos frecuentes
00:27 - 00:36
`BOOLEAN` existe en ambas variantes como valores «verdadero» o «falso», y se usa habitualmente para filtrar;

5. Tipos de datos frecuentes
00:36 - 00:40
y los datos de fecha y hora también tienen varios tipos comunes.

1 https://docs.snowflake.com/en/sql-reference/intro-summary-data-types
6. Tipos de datos SQL de Snowflake: NUMBER
00:40 - 01:08
¿Y qué hay de los tipos de datos exclusivos de Snowflake? En primer lugar, tenemos `NUMBER`, similar al tipo de datos`NUMERIC` de Postgres. Podemos definir la precisión, es decir, el número de dígitos, y la escala, es decir, el número de decimales. Ambos tienen un máximo de 38; si se supera cualquiera de estos valores, se redondeará el resultado, lo que puede provocar una pérdida de precisión.

7. Tipos de datos SQL de Snowflake: TIMESTAMP_LTZ
01:08 - 01:27
TIMESTAMP_LTZ es un tipo de datos exclusivo de Snowflake que almacena información sobre la fecha, la hora y la zona horaria local. Usamos la palabra clave TIMESTAMP_LTZ para definirlo, y los datos se guardan en el formato que se muestra.

8. Conversión de tipos de datos: ¿qué es?
01:27 - 01:33
A veces, puede que tengamos que convertir datos de un tipo a otro, como de cadena a entero.

9. Conversión de tipos de datos: ¿por qué?
01:33 - 01:57
Hay varias razones para hacerlo. Optimiza el rendimiento, por ejemplo, convirtiendo los decimales en números enteros si solo nos interesan los números enteros. Almacenar los datos en el formato correcto garantiza la precisión y la fiabilidad a la hora de analizarlos; Un conjunto de datos coherente y preciso siempre es de mayor calidad.

10. Conversión de tipos de datos: ¿cómo se hace?
01:57 - 02:39
Snowflake ofrece varias formas de convertir tipos de datos. Lo primero es la`CAST()`función. Usamos la palabra clave `CAST`, y luego indicamos los datos de origen o el nombre de la columna y el tipo de datos de destino deseado, separados por la`AS`palabra clave . Por ejemplo, para convertir un`VARCHAR`«80» en un `INT`, usaríamos: `CAST('80' AS INT)`. También podemos usar el operador de dos puntos, que va justo después de los datos de origen o de la columna. Tendría el siguiente aspecto "80'::INT\`.

11. CAST
02:39 - 02:51
Aquí estamos convirtiendo la`order_timestamp`columna a un`DATE`formato. Una vez convertido, solo veremos la fecha del pedido, sin los detalles de la hora y los minutos.

12. CAST resultados
02:51 - 02:57
Esta tabla muestra los datos de la columna original, y la segunda tabla muestra el nuevo formato.

13. Funciones de conversión
02:57 - 03:31
Por otra parte, Snowflake ofrece una serie de funciones de conversión como`TO_VARCHAR` y `TO_DATE`. Vamos a ver`TO_VARCHAR`... Convierte expresiones, como un número o una marca de tiempo, a formato de cadena. Esto resulta útil, por ejemplo, para combinar datos numéricos y de cadena en un identificador único con fines de generación de informes. Escribimos`TO_VARCHAR`y proporcionamos los datos que queremos convertir entre paréntesis, y nos devuelve los datos en`VARCHAR`ese formato.

14. Comprobación de los tipos de datos
03:31 - 03:43
Podemos usar la`DESC TABLE`palabra clave `SELECT`, seguida del nombre de la tabla, para obtener información sobre todas las columnas de una tabla, incluidos sus respectivos tipos de datos.

15. ¡Vamos a practicar!
03:43 - 03:53
¿No te ha parecido estimulante profundizar en los tipos de datos y aprender sobre su conversión? ¡Ahora te toca a ti poner en práctica lo que has aprendido!