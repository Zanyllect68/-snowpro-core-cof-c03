1. Almacenes virtuales: tipos, tamaños y escalado
00:00 - 00:00
En este video profundizamos en los almacenes virtuales — qué tipos existen, cómo están configurados, cómo el tamaño afecta sus costos y cómo adaptar la estrategia de escalamiento correcta a la carga de trabajo correcta. Si te equivocas, o estás pagando de más o estás viendo cómo se rastrean las consultas. Hazlo bien y Snowflake funcionará como se supone que debe hacerlo.

2. Un almacén, muchas cargas de trabajo
00:00 - 00:00
Imagínese un solo almacén manejando todo — un equipo de BI actualizando los paneles, un ingeniero de datos ejecutando una carga por lotes durante la noche, un analista realizando consultas ad hoc y un equipo de ML procesando un gran conjunto de datos. Todos compiten por el mismo cálculo.

3. Un almacén, demasiadas cargas de trabajo
00:00 - 00:00
Esto significa que las consultas comienzan a ponerse en cola, los paneles se ralentizarán y los trabajos por lotes comenzarán a ejecutarse tarde. El instinto es buscar un almacén más grande, pero esa no es la verdadera solución. La respuesta son almacenes separados, uno para cada equipo. De esa manera no hay contención, ni conflictos de programación y ninguna carga de trabajo bloquea a otra. Debido a que Snowflake separa la computación del almacenamiento, crear almacenes adicionales no duplica sus datos. Cada almacén lee desde la misma capa de almacenamiento de forma independiente.

4. Optimizado estándar versus parque de nieve
00:00 - 00:00
Dentro de cada almacén tienes dos tipos para elegir. El estándar cubre la gran mayoría de los casos de uso: consultas SQL, carga de datos e informes de BI. Hay una opción Gen2 más nueva con rendimiento mejorado; si utiliza menos créditos que Gen1 depende de la carga de trabajo, así que pruebe ambas si el costo importa. Los almacenes optimizados para Snowpark están diseñados para cargas de trabajo de Snowpark que consumen mucha memoria. Puede configurar la memoria y la CPU de forma más flexible para esos trabajos. Están disponibles desde tamaño mediano en adelante y cuestan más que un almacén estándar, así que úselos cuando la carga de trabajo realmente necesite espacio adicional.

5. Dimensionamiento de almacenes
00:00 - 00:00
Hay muchas opciones diferentes de tamaño de almacén y puedes crearlas desde SQL. XS maneja consultas ligeras y desarrollo, Large a menudo se adapta a análisis de producción y XL y superiores son para trabajos muy grandes o complejos. El gráfico de la derecha es la misma idea de punto óptimo que verá en la siguiente diapositiva: la misma consulta en Pequeño, Mediano y Grande puede costar aproximadamente los mismos créditos totales porque un almacén más grande termina más rápido. Snowflake también factura por segundo con un mínimo de 60 segundos cuando se inicia un almacén, lo cual es importante para el costo. Eso es lo que hace que “tallar correctamente” sea un hábito, no que “siempre sea más grande”

6. El punto dulce
00:00 - 00:00
Esto es lo que la tabla de créditos por hora no te dice. Ejecute la misma consulta en un almacén pequeño, mediano y grande — los tres consumen aproximadamente los mismos créditos totales, porque el almacén más grande termina el trabajo en menos tiempo. El tiempo de consulta se reduce a la mitad con cada tamaño aumentado, pero el gasto en crédito apenas se mueve. Solo comienza a subir en XL y superiores, donde las ganancias de rendimiento comienzan a estabilizarse. Ese es el punto óptimo — el tamaño de almacén más pequeño donde agregar más cómputo deja de generar retornos proporcionales. Más grande no siempre es más barato si se tiene en cuenta cuánto tiempo dura realmente.

7. Control de costos: suspensión automática y reanudación automática
00:00 - 00:00
Dos configuraciones que controlan directamente sus costos y deben configurarse en cada almacén desde el principio. AUTO_SUSPEND define cuántos segundos de inactividad antes de que el almacén se suspenda automáticamente. Trescientos segundos, también conocidos como cinco minutos, es un valor predeterminado común. AUTO_RESUME = TRUE significa que se activa en el momento en que llega una consulta, sin necesidad de intervención manual. Un almacén que se deja funcionando sin carga de trabajo activa quema créditos continuamente. Estas dos configuraciones son el control de costos más simple que te brinda Snowflake, no las omitas.

8. Almacén multiclúster
00:00 - 00:00
Multi-cluster es la respuesta de Snowflake a las cargas de trabajo de alta concurrencia. Cuando la demanda aumenta, automáticamente surgen clústeres adicionales. Cuando la demanda cae, se suspenden. Usted establece el recuento mínimo y máximo de clústeres, Snowflake se encarga del resto. Multi-cluster es una función de la edición Enterprise y،por lo tanto, no está disponible en la edición estándar.

9. Ampliación de escala versus ampliación de escala
00:00 - 00:00
Ampliar y ampliar resuelve diferentes problemas, y confundirlos es un error común. Si una sola consulta pesada es lenta, generalmente se amplía (un almacén más grande le brinda a esa consulta más recursos). Si se ponen en cola muchas sesiones al mismo tiempo, es posible que un solo clúster más grande no sea la solución; en su lugar, debe escalar con más clústeres para que el trabajo se ejecute en paralelo. Multi-cluster, que acabas de ver, es la forma en que Snowflake agrega clústeres para ese caso de concurrencia.

10. Política económica versus política de escala estándar
00:00 - 00:00
Una vez habilitado el clúster múltiple, usted elige una política de escalamiento. Standard crea un nuevo clúster en el momento en que algo se pone en cola — prioriza el rendimiento sobre los ahorros de crédito. La economía es más conservadora: sólo agrega un clúster si la carga actual lo mantendrá ocupado durante más de seis minutos. Los picos cortos se resuelven por sí solos, sin coste adicional. Desea utilizar Estándar para cargas de trabajo impredecibles, mientras que Economía es para concurrencia constante y predecible. Asegúrese de tener un buen concepto de sus patrones de tráfico antes de elegir la póliza.

11. ¡Vamos a practicar!
00:00 - 00:00
Pongamos a prueba tus conocimientos.