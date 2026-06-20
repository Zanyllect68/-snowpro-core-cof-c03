1. Registro, seguimiento y auditoría
00:00 - 00:26
Hasta ahora, hemos cubierto el control de costos y la protección de datos. Este vídeo cierra el capítulo con un tipo diferente de protección — la capacidad de probar lo sucedido. El equipo de cumplimiento de Claro no sólo necesita datos para estar seguro. Deben demostrar a los auditores que pueden rastrear cada acceso a datos, cada inicio de sesión fallido y cada ejecución de procedimiento hasta un usuario y una hora específicos.

2. El problema de la auditoría
00:26 - 00:55
El equipo de cumplimiento de Claro recibe una solicitud de auditoría: ¿quién accedió a los puntajes crediticios en los últimos noventa días? El equipo de seguridad quiere saber qué procedimientos almacenados se ejecutaron en las primeras horas de una mañana específica. El oficial de cumplimiento quiere saber si algún inicio de sesión provino de fuera de la red corporativa. Estas preguntas requieren un registro completo y consultable que debe existir antes de formular la pregunta.

3. ¿Qué son las tablas de eventos?
00:55 - 01:28
Una tabla de eventos es una tabla especial de Snowflake diseñada para capturar datos de registro y seguimiento emitidos por objetos Snowflake — procedimientos almacenados, funciones de Snowpark y UDF. Lo crea como una tabla normal y luego lo designa como tabla de eventos activos usando ALTER ACCOUNT. A partir de ese momento, los mensajes de registro y seguimiento se escriben en él automáticamente. Debido a que es una tabla Snowflake estándar, se consulta con SQL — sin necesidad de herramientas de registro externas.

4. Niveles de registro
01:28 - 02:07
Los niveles de registro controlan cuántos detalles se escriben en la tabla de eventos. TRACE es el más granular. Captura todas las entradas y salidas de funciones, útil durante el desarrollo pero ruidoso en la producción. DEBUG captura detalles de diagnóstico. INFO registra los hitos normales de ejecución. WARN señala condiciones inesperadas que no detuvieron la ejecución. ERROR registra fallas. FATAL registra fallas críticas que detuvieron la ejecución. En producción, Claro normalmente establecería INFO como el nivel mínimo.

5. Rastreo
02:07 - 02:38
El seguimiento captura la ruta de ejecución a través de un proceso de varios pasos — no mensajes individuales, sino cómo se conectan los pasos. Si la canalización de Claro llama a tres procedimientos almacenados y a una función de Snowpark, el seguimiento muestra cuánto tiempo tomó cada paso y en qué orden se ejecutaron. Los datos de seguimiento se escriben en la misma tabla de eventos que los datos de registro. En el caso de procesos complejos, el rastreo es lo que permite identificar dónde se pierde el tiempo o dónde diverge la ejecución.

6. Uso de LOGIN_HISTORY para auditoría
02:38 - 03:03
Aquí no nos preguntamos cuántos inicios de sesión fallidos ocurrieron, sino si algún inicio de sesión provino de fuera de la red corporativa de Claro. La consulta filtra LOGIN_HISTORY para eventos de inicio de sesión desde direcciones IP fuera del rango corporativo esperado durante los últimos noventa días — quién se autenticó, desde dónde, usando qué método, con cualquier falla claramente visible.

7. QUERY_HISTORY para auditoría
03:03 - 03:33
Aquí QUERY_HISTORY no se trata de encontrar las consultas más lentas — se trata de encontrar qué consultas tocaron una tabla confidencial específica. La consulta filtra cualquier declaración que haga referencia a la tabla de puntajes crediticios de los últimos noventa días y devuelve el usuario, el rol, el almacén y el texto exacto de la consulta. Así es como el equipo de cumplimiento demuestra a un auditor exactamente quién accedió a datos financieros confidenciales, cuándo y qué ejecutó.

8. La pista de auditoría completa
03:33 - 04:12
Estas tres fuentes le dan a Claro un registro de auditoría completo. La tabla de eventos captura el registro operativo: registros y rastros de procedimientos almacenados y funciones de Snowpark. LOGIN_HISTORY cubre la autenticación — quién se conectó, desde dónde y si algún intento falló. QUERY_HISTORY captura cada declaración SQL ejecutada en la cuenta. Juntos responden qué hizo la plataforma, quién inició sesión y qué datos se tocaron. Este es un registro de auditoría que un auditor esperaría, totalmente consultable desde Snowflake.

9. ¡Vamos a practicar!
04:12 - 04:24
Ahora es tu turno. Los ejercicios siguientes le permitirán crear consultas de auditoría en LOGIN_HISTORY y QUERY_HISTORY para responder preguntas de cumplimiento reales para Claro.

