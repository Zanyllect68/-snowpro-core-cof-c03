1. Cifrado, alertas y notificaciones
00:00 - 00:00
Hemos cubierto el control de acceso a nivel de objeto, columna y fila, y herramientas como etiquetado, clasificación, linaje y Trust Center. En este vídeo cerramos la imagen de gobernanza con cifrado, alertas e integraciones de notificaciones.

2. Tres capas de protección
00:00 - 00:00
Incluso con roles y políticas de enmascaramiento establecidas, un oficial de cumplimiento en Claro necesita confianza a un nivel más profundo. ¿Qué pasaría si el almacenamiento subyacente estuviera comprometido? ¿Qué pasaría si de repente un almacén consumiera diez veces sus créditos normales? ¿Qué pasaría si una cuenta de servicio comenzara a consultar tablas que nunca antes había tocado? El cifrado, las alertas y las notificaciones son la respuesta: tres capas que protegen, detectan e informan.

3. Cifrado en reposo y en tránsito
00:00 - 00:00
Snowflake cifra todos los datos automáticamente, sin necesidad de configuración. Los datos en reposo utilizan AES-256. Las claves de cifrado se rotan automáticamente según un cronograma regular, lo que limita la exposición si una clave se ve comprometida. Los datos en tránsito entre un cliente y Snowflake, o entre los servicios internos de Snowflake, están protegidos mediante TLS 1.2 o superior. Cada puntaje crediticio y registro de pago en Claro está cifrado en cada etapa de su viaje a través de Snowflake.

4. Opciones clave de gestión
00:00 - 00:00
De forma predeterminada, Snowflake administra las claves de cifrado en su nombre. Para la mayoría de las organizaciones esto es suficiente. Pero los servicios financieros, la atención médica y las organizaciones gubernamentales pueden exigir que el cliente posea él mismo la clave de cifrado maestra. Snowflake admite esto mediante la integración con servicios de administración de claves en la nube: AWS KMS, Azure Key Vault y GCP KMS. Cuando un cliente posee la clave maestra, conserva el control final —, incluida la capacidad de revocar el acceso a sus datos por completo revocando la clave.

5. Tri-Secreto Seguro
00:00 - 00:00
Tri-Secret Secure lleva las claves administradas por el cliente un paso más allá. En una configuración estándar, incluso con una clave administrada por el cliente, las propias credenciales de Snowflake teóricamente podrían acceder a los datos. Tri-Secret Secure elimina esto al requerir tres cosas simultáneamente: la clave administrada del propio Snowflake, la clave del cliente guardada en su KMS en la nube y la autenticación exitosa del usuario a través de Snowflake. Si el cliente revoca su clave, Snowflake no podrá acceder a los datos. Está disponible en la edición Business Critical y superiores.

6. ¿Qué es una alerta de copo de nieve?
00:00 - 00:00
Una alerta de Snowflake evalúa una condición SQL y actúa cuando la respuesta es sí. Hay dos modos de activación: las alertas programadas se ejecutan en un intervalo regular usando CRON o una configuración simple de minutos/hora, y las alertas basadas en eventos se activan cuando llegan nuevos datos a una transmisión, sin necesidad de un cronograma fijo. Cuando la condición se evalúa como verdadera, la alerta ejecuta una acción, normalmente una notificación. En Claro, una alerta podría estar atenta a patrones de inicio de sesión inusuales o anomalías en los registros de pago entrantes.

1 https://docs.snowflake.com/en/user-guide/alerts
7. Estructura de alerta en SQL
00:00 - 00:00
CREATE ALERT define el objeto y le asigna un almacén y un cronograma. El bloque IF contiene la condición SELECT que devuelve un resultado si se produjo algún intento fallido de inicio de sesión en la última hora. El bloque THEN define lo que sucede cuando la condición es verdadera: se envía una notificación utilizando SYSTEM$SEND_SNOWFLAKE_NOTIFICATION. La estructura es consistente en todas las alertas: cronograma, condición, acción. Para el monitoreo de crédito de almacén, verá una herramienta más específica en el próximo capítulo: monitores de recursos.

8. Integraciones de notificaciones
00:00 - 00:00
Las alertas se vuelven útiles cuando llegan a las personas adecuadas. Snowflake conecta alertas a sistemas externos a través de integraciones de notificaciones — objetos preconfigurados que definen un destino. Los destinos admitidos incluyen correo electrónico, colas de proveedores de nube como Amazon SNS, Google Cloud Pub/Sub y Azure Event Grid, y webhooks para herramientas como Slack, PagerDuty y Microsoft Teams. En Claro, las alertas de inicio de sesión fallidas pueden dirigirse a un canal de Slack mientras que los hallazgos de cumplimiento van a PagerDuty. Las integraciones de notificaciones se crean por separado de las alertas, manteniendo el enrutamiento configurable y la lógica de alerta limpia.

9. ¡Vamos a practicar!
00:00 - 00:00
Esto resume el cifrado, las alertas y las notificaciones. Pongamos estos conceptos en práctica.