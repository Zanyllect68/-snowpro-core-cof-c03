1. Características de Snowflake Cortex y ML
00:00 - 00:00
En este vídeo vemos Snowflake Cortex: la capa de IA incorporada de Snowflake.

2. Descripción general de la corteza del copo de nieve
00:00 - 00:00
Verá cómo ejecutar tareas de lenguaje como analizar documentos, clasificar texto y resumir contenido, todo sin salir de SQL. Y veremos cómo Snowflake ML extiende eso al modelado predictivo.

1* Material de aprendizaje de SNowflake
3. El problema de los datos no estructurados
00:00 - 00:00
Los equipos de patrulla de esquí de Snowy Peak envían informes de turno en formato PDF al final de cada turno. La aplicación recopila opiniones de usuarios en tres idiomas. Los comentarios de los clientes llegan como texto de formato libre que debe clasificarse en categorías antes de que alguien pueda actuar en consecuencia. Todos estos datos llegan a Snowflake, pero no puedes escribir un SELECT en un PDF. No es posible clasificar automáticamente texto de formato libre con SQL estándar. Esa brecha es lo que Cortex está diseñado para cerrar.

4. ¿Qué es Snowflake Cortex?
00:00 - 00:00
Cortex le brinda acceso a grandes modelos de lenguaje de varios proveedores, incluidos Claude de Anthropic, Meta (Llama), Mistral, OpenAI, incluida la familia GPT cuando esté disponible, Google Gemini cuando esté disponible y Snowflake Arctic, todos alojados y administrados dentro de Snowflake. No hay una clave API externa para configurar en el patrón básico y sus datos no salen de la plataforma para esas llamadas. Invoca funciones de Cortex de la misma manera que lo haría con cualquier otra función SQL. Ése es el diseño clave: IA, donde ya se encuentran tus datos.

5. Análisis de documentos
00:00 - 00:00
El análisis es la forma de llegar desde el archivo “en un escenario” a los valores “que SQL puede usar” Un PDF (o documento respaldado por imágenes) no es una tabla: primero lo analiza con `SNOWFLAKE.CORTEX.PARSE_DOCUMENT` o el más nuevo `AI_PARSE_DOCUMENT` donde su cuenta lo admite. La función devuelve una salida estructurada (a menudo una `VARIANTE`) para que pueda extraer texto con los mismos patrones `:` y `::` que utilizó para JSON anteriormente en el curso, y luego pasar ese texto a otras funciones Cortex o SQL. `PARSE_DOCUMENT` es un primer paso típico para cualquier cosa que comience como un archivo.

6. Funciones SQL de Cortex: clasificar y traducir
00:00 - 00:00
Ahora cubriremos algunas otras funciones SQL de corteza AI comúnmente utilizadas. La lista completa de funciones está en constante crecimiento, así que asegúrese de mantenerse al día con la documentación de Snowflake para ver qué hay disponible. Ahora volvamos a las funciones. Una vez que tenga texto, una variedad de funciones SQL pueden actuar sobre él. CLASSIFY_TEXT toma una cadena y una matriz de etiquetas de categorías y devuelve la mejor coincidencia — le pasa un informe de patrulla y una lista de niveles de gravedad, regresa con una etiqueta. TRANSLATE toma texto y dos códigos de idioma: pasa una revisión en francés y vuelve al inglés.

7. Funciones SQL de Cortex: completar y resumir
00:00 - 00:00
COMPLETO es el más abierto: dale un nombre de modelo y un mensaje y genera una respuesta — útil siempre que la tarea no se ajuste a un patrón predefinido. Y por último RESUMIR condensa un cuerpo de texto en una versión más corta.

8. Cortex Search y Cortex Analyst
00:00 - 00:00
Repasemos otras características de la IA de Cortex. Cortex Search ejecuta consultas de similitud semántica sobre el texto del documento —, por lo que en lugar de coincidir con palabras clave exactas, encuentra contenido que significa algo similar. Para Snowy Peak, eso podría significar sacar a la luz todos los informes de incidentes relacionados con las condiciones de visibilidad, incluso si no usan esa frase exacta. Cortex Analyst va más allá: traduce preguntas en inglés sencillo a SQL, de modo que un gerente de producto puede preguntar qué complejos turísticos tuvieron más incidentes el invierno pasado sin escribir una línea de código.

9. Ciclo de vida de Snowflake ML
02:36 - 03:10
Snowflake ML agrega cargas de trabajo predictivas sobre los mismos datos y gobernanza que ya utiliza. Un pronóstico no es un `SELECT` de una sola línea como lo son los informes ad hoc: primero define un modelo y luego llama al ` del modelo!Método FORECAST`. Eso mantiene el entrenamiento separado de la puntuación, similar a otros servicios de ML. Como ejemplo utilizas `CREA O REEMPLAZA SNOWFLAKE.ML.FORECAST con el nombre de tu modelo, luego `¡LLAME a my_model!PRONOSTICAR y especificar el período de pronóstico. Haga coincidir siempre la sintaxis actual en la documentación de su cuenta. Para obtener más información, la descripción general oficial de las funciones de ML en la documentación de Snowflake enumera pronósticos, detección de anomalías y funciones relacionadas con la sintaxis más reciente.

10. ¡Vamos a practicar!
00:00 - 03:10
¡Pongamos a prueba tus conocimientos!