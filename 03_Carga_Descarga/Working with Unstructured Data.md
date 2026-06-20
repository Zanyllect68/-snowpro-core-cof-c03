1. Trabajar con datos no estructurados
00:00 - 00:00
En este vídeo veremos cómo Snowflake maneja archivos no estructurados.

2. Más allá de las tablas
00:00 - 00:00
Snowflake se construyó originalmente alrededor de tablas estructuradas, pero los equipos almacenan cada vez más archivos PDF, imágenes, audio y otros documentos junto con esos datos. No puede consultar un PDF sin procesar como una tabla de filas/columnas, pero Snowflake le brinda etapas, catálogos y patrones de acceso para que los archivos permanezcan en la plataforma. Más adelante en su camino de aprendizaje, puede combinar estos archivos con funciones Cortex y LLM para búsqueda y enriquecimiento; aquí nos centramos en el almacenamiento y la gobernanza.

3. Etapas: La zona de aterrizaje de los archivos
00:00 - 00:00
Ya hemos introducido el concepto de etapas. Las etapas internas contienen archivos administrados y dirigidos por Snowflake. Las etapas externas hacen referencia a archivos ubicados en lugares como S3, Azure Blob Storage o Google Cloud. Para los datos no estructurados, la etapa es donde se encuentran los archivos. A diferencia de muchas tuberías estructuradas, el escenario suele ser el hogar de esos objetos, no solo una zona de aterrizaje temporal.

4. Tablas de directorio
00:00 - 00:00
Una tabla de directorio es una capa de metadatos que Snowflake genera automáticamente encima de un escenario. Cuando lo habilitas, Snowflake comienza a catalogar cada archivo en esa etapa — su nombre, tamaño, fecha de última modificación y una URL para acceder a él.

5. Sintaxis de tablas de directorio
00:00 - 00:00
Para configurar uno, crea un escenario con la opción de directorio habilitada. El parámetro DIRECTORY equals ENABLE equals TRUE es lo que le indica a Snowflake que comience a rastrear archivos tan pronto como aterricen. No construyes la tabla tú mismo: Snowflake la genera automáticamente una vez que se establece esa bandera. Cuando llegan nuevos archivos al escenario, la tabla de directorios no se actualiza por sí sola de forma predeterminada. Utiliza ALTER STAGE con la palabra clave REFRESH para sincronizarlo.

6. Tablas de directorio
00:00 - 00:00
Eso le dice a Snowflake que escanee el escenario y actualice el catálogo con cualquier cosa nueva. También puedes configurar la actualización automática, pero el comando manual es el que utilizarás durante las pruebas y las cargas ad hoc.

7. Consultar una tabla de directorio
00:00 - 00:00
Puede consultar una tabla de directorio utilizando la función DIRECTORIO con el nombre artístico prefijado con el símbolo @. Aquí extraemos el nombre del archivo, el tamaño y la fecha de la última modificación de la etapa Snowy Peak. El equipo puede usar esto para auditar lo que hay en la etapa, detectar archivos obsoletos o alimentar cualquier proceso posterior que necesite saber qué informes están disponibles.

8. URL previamente firmadas
00:00 - 00:00
Las tablas del directorio enumeran lo que hay en una etapa. Cuando algo fuera de Snowflake necesita acceso temporal a un archivo, Snowflake puede exponer varios patrones de URL según la integración: URL de etapa, URL de archivo con alcance, URL firmadas previamente y ayudantes relacionados. Se diferencian en su alcance, vida útil y quién puede acuñarlos. `GET_PRESIGNED_URL` es el patrón común para un enlace HTTPS compartible y de tiempo limitado a un objeto. Pasas el escenario, la ruta del archivo y la vida útil en segundos. El enlace funciona hasta que expira, lo que resulta útil para socios o aplicaciones que no tienen inicios de sesión en Snowflake. Utilice el tipo de URL correcto para su modelo de seguridad. Consulte la documentación de Snowflake para obtener la matriz completa.

9. ¡Vamos a practicar!
00:00 - 00:00
Apliquemos lo que has aprendido sobre cómo trabajar con datos no estructurados.