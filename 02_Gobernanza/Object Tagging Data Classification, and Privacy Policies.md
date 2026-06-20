1. Etiquetas de objetos, clasificación de datos y políticas de privacidad
00:00 - 00:21
Las políticas de enmascaramiento dinámico de datos y acceso a filas suponen que ya sabe qué columnas contienen datos confidenciales. A escala de Claro — cientos de tablas, múltiples esquemas, una base de usuarios global — eso no siempre es cierto. Este vídeo cubre las herramientas que Snowflake le brinda para encontrar, etiquetar y proteger sistemáticamente datos confidenciales.

2. El problema de la escala
00:21 - 00:51
Claro tiene cientos de mesas. Algunos contienen datos operativos sin sensibilidad. Otros contienen información personal identificable, como nombres y correos electrónicos. Si confía en que las personas identifiquen manualmente cada columna confidencial, terminará con una imagen incompleta que se vuelve obsoleta cada vez que se agrega una nueva tabla. El enfoque de Snowflake: etiqueta lo que sabes con etiquetas y deja que Snowflake encuentre lo que no con la clasificación de datos.

3. ¿Qué es una etiqueta de objeto?
00:51 - 01:37
Una etiqueta de objeto es una etiqueta de metadatos adjunta a un objeto Snowflake. No cambia lo que hace la columna ni quién puede consultarla, le adjunta metadatos de búsqueda. Las etiquetas tienen muchos usos: el etiquetado de sensibilidad es un ejemplo común, pero las etiquetas también se utilizan para la asignación de costos, la propiedad de datos y el seguimiento del cumplimiento. Las etiquetas son pares clave-valor. Puede crear una etiqueta llamada sensibilidad con valores PII, Confidencial e Interno, luego aplicar sensibilidad igual a PII a las columnas de correo electrónico y puntaje crediticio de Claro. Cualquier persona con acceso a los metadatos de la cuenta ahora puede encontrar cada columna PII sin inspeccionar las tablas individualmente.

4. Creación y aplicación de una etiqueta
01:37 - 02:16
Las etiquetas son objetos a nivel de esquema،viven dentro de un esquema como una tabla o vista, por lo que heredan el control de acceso del esquema. Primero, cree la etiqueta con valores permitidos definidos: esto evita que las etiquetas de texto libre se vuelvan inconsistentes con el tiempo. Luego aplíquelo a la columna de correo electrónico de Claro usando ALTER TABLE MODIFY COLUMN SET TAG. TAG_REFERENCES le permite consultar qué objetos han sido etiquetados y con qué valores. Esa consulta le brinda al equipo de cumplimiento una vista de todo lo etiquetado como PII.

1 https://docs.snowflake.com/en/user-guide/object-tagging/introduction
5. Herencia de etiquetas
02:16 - 02:38
Las etiquetas admiten herencia. Aplique una etiqueta a nivel de esquema y cada tabla y columna dentro de ese esquema la hereda automáticamente — útil para etiquetado masivo en lugar de etiquetar cientos de columnas individuales. Las etiquetas aplicadas en un nivel inferior anulan las heredadas, por lo que aún puedes ser específico cuando sea necesario.

6. ¿Qué es la clasificación de datos?
02:38 - 03:16
Las etiquetas de objetos se aplican manualmente — dependen de que alguien sepa que una columna es sensible. La clasificación de datos es la respuesta de Snowflake a lo que no sabes. Escanea sus tablas automáticamente, examinando nombres de columnas, tipos de datos y valores de muestra, luego identifica columnas que probablemente contengan datos confidenciales y las asigna a categorías PII estándar: nombre, correo electrónico, teléfono, números de pasaporte. Para Claro, así es como el equipo de cumplimiento encuentra columnas confidenciales en tablas creadas antes de que existiera cualquier proceso de gobernanza.

7. Cómo implementar la clasificación
03:16 - 03:41
Classification results are surfaced in Snowsight. You can run classification directly on a table from the catalog, or access it through the Trust Center under the Data Security section. Either way, you can see which columns Snowflake identified as sensitive and what category each maps to. Classification gives you a starting point. Tags let you refine and extend it.

1 https://docs.snowflake.com/en/user-guide/classify-ui-trust-center
8. Privacy Policies
03:41 - 04:21
Las etiquetas etiquetan datos confidenciales. La clasificación lo encuentra. Las políticas de privacidad completan el panorama al vincular la clasificación con la protección. Una política de privacidad vincula una categoría de clasificación —como el correo electrónico— a una política de enmascaramiento. Cuando Snowflake clasifica una columna como correo electrónico, la política de enmascaramiento se aplica automáticamente. En Claro, cualquier tabla nueva con una columna de correo electrónico queda enmascarada para roles no privilegiados sin que el equipo de cumplimiento tenga que conectar manualmente una política cada vez.

9. ¡Vamos a practicar!
00:00 - 04:21
Es hora de poner en práctica el etiquetado y la clasificación. Vamos.