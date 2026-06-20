1. Herramientas para cada equipo
00:00 - 00:00
Bienvenidos a nuestro cuarto y último capítulo de este curso. En el vídeo anterior, cubrimos cómo trabajar con datos no estructurados. Ahora exploraremos las herramientas en Snowflake que se adaptan a las necesidades de diferentes equipos de datos.

2. Tres casos de uso diferentes
00:00 - 00:00
En Snowy Peak, el equipo de datos ha crecido y todos necesitan algo ligeramente diferente de Snowflake. El ingeniero de datos quiere ejecutar un modelo de abandono de Python en millones de filas de suscripción. El analista de datos quiere explorar los registros de sesión de anoche usando SQL y Python en el mismo lugar, sin cambiar de herramienta. Y el gerente de producto quiere tener acceso a un panel de control en vivo que pueda ejecutarse y revisarse todas las mañanas. Estos usuarios tienen casos de uso muy diferentes. Veamos qué puede ofrecer Snowflake a cada uno de estos usuarios.

3. Cuadernos de copos de nieve
00:00 - 00:00
Snowflake Notebooks vive dentro de Snowsight, por lo que no requiere instalación ni configuración adicional. Un cuaderno le ofrece tres tipos de celdas diferentes (similares a los cuadernos Jupyter): Markdown para anotaciones, SQL para escribir consultas y Python para todo lo demás.

4. Cuadernos de copos de nieve
00:00 - 00:00
Una cosa que los hace particularmente útiles: puedes definir una variable en una celda de Python y hacer referencia a ella dentro de una celda de SQL usando la sintaxis Jinja. Se trata de dos tirantes rizados alrededor del nombre de la variable. Esto significa que puede escribir la consulta, anotar sus hallazgos y agregar una visualización, todo en un solo lugar. Los portátiles necesitan un almacén virtual activo para ejecutar celdas ejecutables. Inicie la sesión y el cálculo se activará automáticamente. Esta es la herramienta para que el analista investigue aquellos patrones de sesión en los que puede combinar SQL y Python en un único flujo de trabajo.

5. Parque de nieve
00:00 - 00:00
Snowflake ofrece una biblioteca para desarrolladores llamada Snowpark: está disponible para Python, Scala y Java, donde el código se ejecuta dentro de Snowflake. La idea es que el código vaya a los datos, no al revés. Esto significa que no es necesario trasladar datos a un entorno local o a una infraestructura externa para su gestión. Eso es lo que hace que Snowpark sea adecuado para el trabajo de producción: canalizaciones ETL nocturnas, transformaciones ML por lotes, funciones personalizadas a escala. Si el ingeniero de datos de Snowy Peak necesita calificar el riesgo de abandono de cada suscriptor activo a las 2 a. m., ¡esta es la herramienta para ellos!

6. Iluminado por la corriente en Snowflake
00:00 - 00:00
Es posible que hayas encontrado Streamlit en Python antes, Streamlit en Snowflake es una forma de crear aplicaciones interactivas que pueden ejecutarse dentro de Snowflake. Le permite desarrollar su aplicación en Python, implementarla dentro de Snowflake y brindar acceso a cualquier miembro del equipo. Esto significa que todos los datos permanecen en la plataforma y estás construyendo algo que puedes compartir con otros miembros del equipo.

7. ¿Qué herramienta, cuándo?
00:00 - 00:00
¿Cómo decidir qué herramientas utilizar? Bueno, cuando estás explorando datos y mezclando SQL, Python y Notes en un solo documento, Notebooks es tu mejor opción. Si está desarrollando código de producción, como canales de datos y modelos que se ejecutan de manera confiable a escala, utilice Snowpark. Por último, cuando necesites crear aplicaciones interactivas que puedas compartir con tu equipo, utiliza Streamlit.

8. ¡Vamos a practicar!
00:00 - 00:00
¡Pon en práctica tus conocimientos sobre las diferentes herramientas!