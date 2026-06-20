1. Monitores de recursos y cálculo de crédito
00:00 - 00:00
En este capítulo nos centramos en un tipo diferente de riesgo: el coste. El modelo informático de Snowflake es flexible y potente, pero el gasto puede crecer rápidamente si no se gestiona. Este video cubre cómo funcionan los créditos, cómo calcular cuánto cuesta un almacén y cómo los monitores de recursos le brindan control sobre el consumo antes de que se convierta en un problema.

2. El problema del costo
00:00 - 00:00
El equipo de datos de Claro realiza docenas de consultas al día en varios almacenes. Todo lo que se necesita es que un analista inicie una costosa consulta ad hoc un viernes por la tarde y la deje funcionando. Sin controles de gasto establecidos, se trata de una factura inesperada e importante. Los monitores de recursos son la respuesta de Snowflake.

3. ¿Qué es un crédito Snowflake?
00:00 - 00:00
Un crédito Snowflake es la unidad de consumo computacional. Un crédito equivale a una hora de funcionamiento continuo de un almacén Standard Gen 1 X-Small, pero el consumo de crédito depende tanto del tipo como del tamaño del almacén. Los almacenes más grandes consumen más créditos por hora en un patrón multiplicativo. Los créditos sólo se consumen mientras un almacén está en funcionamiento activo. La suspensión automática detiene el consumo, aunque tenga en cuenta que un intervalo de suspensión más largo permite que los datos permanezcan almacenados en caché, lo que puede mejorar el rendimiento de las consultas para cargas de trabajo repetidas. Es un equilibrio que vale la pena considerar para cada almacén.

4. Consumo de crédito por tamaño de almacén
00:00 - 00:00
Para un almacén estándar de Generación 1, X-Small es la línea de base con un crédito por hora. Pequeño son dos. El mediano es cuatro. El patrón continúa con cada paso duplicando aproximadamente la tarifa por hora. Los almacenes Gen 2 tienen diferentes tarifas que varían según el proveedor de nube, y Snowflake también ofrece almacenes optimizados para Snowpark con su propio cronograma de crédito. Para conocer las cifras actuales de todos los tipos de almacenes, consulte siempre la Tabla de consumo de servicios de Snowflake.

1 https://www.snowflake.com/legal-files/CreditConsumptionTable.pdf
5. Advertencias importantes sobre la facturación
00:00 - 00:00
Dos advertencias que vale la pena conocer. El uso del almacén virtual se factura por segundo, con un mínimo de un minuto cada vez que se inicia el almacén, por lo que una consulta que se ejecuta durante diez segundos aún cuesta un minuto completo. La capa de servicios en la nube de Snowflake se encarga de la autenticación, la optimización de consultas y la gestión de metadatos. Consume créditos, pero esos créditos solo se cobran si el uso de los servicios en la nube excede el diez por ciento de la computación diaria de su almacén. Por debajo de ese umbral, los servicios en la nube están efectivamente incluidos.

6. ¿Qué es un monitor de recursos?
00:00 - 00:00
Un monitor de recursos es un objeto Snowflake que observa el consumo de crédito y actúa cuando cruza un umbral. Usted define una cuota de crédito —por ejemplo quinientos créditos al mes— y adjunta el monitor a un almacén o a toda la cuenta. A medida que el almacén consume créditos, el monitor realiza un seguimiento del progreso respecto de la cuota. Cuando el consumo alcanza un porcentaje definido, el monitor toma medidas: una notificación, una suspensión o una parada inmediata.

7. Acciones del monitor de recursos
00:00 - 00:00
Los monitores de recursos admiten tres tipos de acciones. Notify envía una alerta pero el almacén sigue funcionando, útil como alerta temprana. Suspender detiene el almacén una vez que se completa la declaración actual. Suspender Se detiene inmediatamente a mitad de la ejecución, cancelando las consultas en ejecución. Se pueden establecer múltiples umbrales en un solo monitor. Por ejemplo, un patrón común de Claro: notificar al setenta y cinco por ciento, suspender al noventa, suspender inmediatamente al cien, dando al equipo la oportunidad de reaccionar antes de que se interrumpan las operaciones.

8. Monitores de nivel de cuenta vs. de almacén
00:00 - 00:00
Los monitores de recursos se aplican en dos niveles. Un monitor a nivel de cuenta rastrea el consumo total de crédito en cada almacén — una única barandilla para el presupuesto general. Un monitor a nivel de almacén tiene alcance para un almacén, lo que le otorga a cada equipo su propia cuota de crédito de forma independiente. Los dos niveles pueden coexistir. Claro podría tener un monitor a nivel de cuenta como techo rígido y monitores individuales a nivel de almacén para los equipos de análisis, ingeniería de datos y cumplimiento.

9. ¡Vamos a practicar!
00:00 - 00:00
Ahora es tu turno. Pondrás en práctica los monitores de recursos y los cálculos de crédito en los próximos ejercicios.