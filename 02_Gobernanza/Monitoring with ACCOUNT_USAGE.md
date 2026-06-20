1. Monitoreo con ACCOUNT_USAGE
00:00 - 00:00
Los monitores de recursos son barandillas proactivas. Pero el líder de la plataforma de datos de Claro también necesita mirar atrás: entender qué sucedió, cuánto costó y si la cuenta funciona de manera eficiente. Para eso está ACCOUNT_USAGE. Este video cubre cuál es el esquema, en qué se diferencia de INFORMATION_SCHEMA y qué vistas responden las preguntas que más importan.

2. El problema del seguimiento
00:00 - 00:00
Al final de cada mes, el líder de la plataforma de datos de Claro necesita respuestas: qué almacenes cuestan más, si hubo consultas descontroladas que deberían haberse detectado, si el almacenamiento está dentro del presupuesto, ¿se produjeron patrones de inicio de sesión inusuales? Estas preguntas requieren datos históricos a nivel de cuenta — agregados entre todos los usuarios, todos los almacenes y todas las bases de datos. Eso es exactamente lo que proporciona ACCOUNT_USAGE.

3. ¿Qué es ACCOUNT_USAGE?
00:00 - 00:00
ACCOUNT_USAGE es un esquema dentro de la base de datos del sistema SNOWFLAKE que Snowflake mantiene para cada cuenta. Contiene vistas que exponen datos históricos: consultas ejecutadas, créditos consumidos, almacenamiento utilizado, inicios de sesión registrados, etc. Dos cosas que debe saber de antemano: los datos tienen una latencia de hasta tres horas, por lo que no son adecuados para el monitoreo en tiempo real y la mayoría de las vistas retienen datos durante 365 días, lo que le brinda un año completo de historial para consultar.

4. USO_CUENTA vs ESQUEMA_INFORMACIÓN
00:00 - 00:00
La diferencia fundamental es el tiempo. INFORMATION_SCHEMA refleja el estado actual de su base de datos con baja latencia: qué tablas existen, qué columnas tienen, qué privilegios existen en este momento. ACCOUNT_USAGE le muestra el historial: lo que sucedió en la cuenta a lo largo del tiempo, incluidos los objetos que desde entonces se eliminaron, pero con un retraso de hasta tres horas. Si necesita auditar quién consultó una tabla que ya no existe, solo ACCOUNT_USAGE puede ayudarlo.

5. HISTORIA_MEDICIÓN_ALMACÉN
00:00 - 00:00
WAREHOUSE_METERING_HISTORY responde: ¿qué almacenes consumieron más créditos? Esta consulta agrega los créditos totales utilizados por almacén durante los últimos treinta días y los clasifica por consumo. En Claro, así es como el líder de la plataforma de datos identifica qué almacén del equipo genera la mayor parte del gasto mensual y si funciona más de lo que justifica la carga de trabajo.

6. CONSULTA_HISTORIAL
00:00 - 00:00
QUERY_HISTORY registra cada consulta ejecutada en la cuenta: quién la ejecutó, en qué almacén, cuánto tiempo tomó y cuántos datos escaneó. Esta consulta muestra las diez consultas de mayor duración de los últimos siete días. En Claro, así es como el líder de la plataforma encuentra candidatos para la optimización: los bytes grandes escaneados a menudo indican que falta agrupación o uniones ineficientes.

7. ALMACENAMIENTO_USO
00:00 - 00:00
STORAGE_USAGE rastrea cuánto almacenamiento consume la cuenta a lo largo del tiempo, tanto almacenamiento de datos activo como almacenamiento a prueba de fallas. Los valores sin procesar están en bytes; dividiéndolos por 1024 a la potencia de tres conversiones a gigabytes. En Claro, esto revela si el almacenamiento total está creciendo al ritmo esperado y si el almacenamiento a prueba de fallas, el búfer de recuperación de siete días en las tablas permanentes, está agregando un costo significativo. La seguridad contra fallos a menudo se pasa por alto, pero puede ser importante para cuentas con tablas grandes y alta rotación de datos.

8. HISTORIAL_INICIO DE SESIÓN
00:00 - 00:00
LOGIN_HISTORY registra cada intento de inicio de sesión en la cuenta, exitoso o no. El filtrado de filas donde error_code no es nulo aísla los intentos fallidos de inicio de sesión. En Claro, un aumento en los inicios de sesión fallidos de un tipo de cliente desconocido o fuera del horario comercial es una señal temprana que vale la pena investigar.

9. ¡Vamos a practicar!
00:00 - 00:00
Ahora es tu turno. Los ejercicios siguientes le permitirán consultar ACCOUNT_USAGE para obtener información sobre costos y uso de la cuenta de Claro.