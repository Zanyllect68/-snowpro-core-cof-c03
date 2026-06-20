1. Linaje de datos y centro de confianza
00:00 - 00:00
La gobernanza no se trata sólo de bloquear cosas —, también se trata de visibilidad. Saber de dónde provienen sus datos, qué depende de ellos y si la configuración de seguridad de su cuenta hace lo que usted cree que hace. Este vídeo cubre Data Lineage y el Trust Center.

2. El problema de la visibilidad
00:00 - 00:00
Imagine que el panel de cumplimiento de Claro deja de devolver datos. En algún lugar río arriba, algo cambió — pero ¿qué? Sin un mapa de cómo se conectan los objetos, estás rastreando dependencias manualmente. Ahora imagine una auditoría de seguridad preguntando qué usuarios tienen acceso a ACCOUNTADMIN y si las cuentas de servicio se autentican sin MFA. Sin una vista centralizada, responder a eso significa consultar varias tablas del sistema y esperar que no se haya pasado por alto nada. El linaje de datos y el Trust Center hacen que ambos problemas sean rastreables.

3. ¿Qué es el linaje de datos?
00:00 - 00:00
El linaje de datos es un mapa de relaciones de objetos en su cuenta Snowflake. Para cualquier objeto dado — una vista, una tabla, una tabla dinámica — el linaje le dice dos cosas: ¿de qué depende este objeto y qué depende de este objeto?

4. Lectura del gráfico de linaje en Snowflake
00:00 - 00:00
En Snowsight, el linaje se visualiza como un gráfico. Los objetos ascendentes aparecen a la izquierda: sus datos de origen. Las dependencias descendentes aparecen a la derecha: los modelos, conjuntos de datos y resultados que dependen de ellas. Siga el flujo de izquierda a derecha y podrá rastrear exactamente cómo se mueven los datos a través de su canalización: desde tablas de origen sin procesar, pasando por ingeniería de funciones, hasta conjuntos de datos empaquetados y, finalmente, modelos entrenados. Si algo cambia aguas arriba, digamos una actualización de esquema o una columna renombrada, puedes ver inmediatamente todo lo que podría verse afectado aguas abajo. Análisis de impacto en segundos, en lugar de horas de rastreo manual.

5. Historial de acceso
00:00 - 00:00
Además del linaje, Snowflake registra el historial de acceso, un registro de qué objetos fueron accedidos, por qué usuario y en qué momento. Esto se encuentra en ACCOUNT_USAGE en ACCESS_HISTORY. Captura no sólo el acceso directo a la tabla sino también el acceso indirecto a través de vistas: si un analista consulta una vista que lee una tabla confidencial, se registra ese acceso subyacente. Para el equipo de cumplimiento de Claro, Access History responde preguntas de auditoría como: ¿quién accedió a la tabla de puntajes crediticios en los últimos 30 días y se produjo algún acceso fuera del horario comercial?

6. ¿Qué es el Trust Center?
00:00 - 00:00
El Trust Center es el centro de monitoreo de seguridad integrado de Snowflake. Ejecuta comprobaciones automatizadas de la configuración de su cuenta y muestra hallazgos donde su configuración no se alinea con las recomendaciones de seguridad de Snowflake. Más allá del monitoreo de configuración, Trust Center también muestra los hallazgos de Clasificación de datos confidenciales en su sección Seguridad de datos, para que pueda descubrir la exposición a PII y las brechas de seguridad desde el mismo lugar. Piense en ello como un control periódico del estado de seguridad: no detecta amenazas en tiempo real, señala brechas de configuración. Para Claro, eso podría significar que ACCOUNTADMIN se otorga a más usuarios de lo recomendado, o que no se aplica MFA para roles privilegiados.

7. Paquetes y hallazgos del escáner
00:00 - 00:00
Los controles del Trust Center están organizados en paquetes de escáner. El CIS Snowflake Benchmark se corresponde con las recomendaciones estándar de la industria del Centro para la Seguridad en Internet. Snowflake Security Essentials cubre las comprobaciones de referencia propias de Snowflake. Threat Intelligence es el tercer paquete, identifica usuarios riesgosos y patrones de actividad sospechosos. También se pueden crear escáneres personalizados para requisitos específicos de la organización. Cada paquete produce hallazgos clasificados por gravedad. Un hallazgo no es una infracción. Es una brecha de configuración. El Centro de Confianza te dice qué mirar; lo que hagas al respecto depende de tu equipo de seguridad.

1 https://docs.snowflake.com/en/user-guide/trust-center/overview#scanner-packages
8. Actuando en función de los hallazgos
00:00 - 00:00
Cada hallazgo del Trust Center incluye un resumen de la violación y una reparación recomendada. Por ejemplo, un hallazgo podría recomendar migrar a los usuarios humanos para que no inicien sesión solo con contraseña moviendo a todos los usuarios a SSO y deshabilitando las cuentas que no hayan iniciado sesión en los últimos 90 días. El Trust Center no soluciona las cosas por usted, pero le brinda una lista clara y priorizada de lo que necesita atención y le indica la documentación para llevarlo a cabo.

9. ¡Vamos a practicar!
00:00 - 00:00
Ahora es tu turno de explorar el linaje y los conceptos del Trust Center. Vamos a practicar.