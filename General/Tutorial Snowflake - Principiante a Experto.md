¿Qué es Copo de Nieve?
Si alguien me pidiera que descriptiera a Snowflake con el menor número de palabras posible, elegante estas:

Almacenes de datos
Datos a gran escala
Nube múltiple
Separación
Escalable
Flexible
Simple
Si querían que me expliqueara, encadenaba las palabras así:

Copo de nieve es una plataforma en la nube de datos de IA muy popular. Destaca entre sus competidores por su capacidad para manejar datos y cargas de trabajo a gran escala con mayor rapidez y eficacia. Su rendimiento superior procede de su arquitectura única, que utiliza capas separadas de alojamiento y cálculo, lo que le permite ser increíblemente flexible y escalable. Ademas, se integra de forma nativa con múltiples probadores de nubes. A pesar de estas funciones avanzadas, sigue siendo sencillo de aprender y aplicar.

Si piden aún más detalles, bueno, entonces escribe este tutorial. Si eres totalmente nuevo en el tema, nuestro curso Introducción a Snowflake es un excelente punto de partida.

¿Por qué utilizar Copo de Nieve?
Snowflake da servicio a más de 8.900 clientes en todo el mundo y proceso 3.900 millones de consultas al día. Ese tipo de estadísticas de uso no es una coincidencia ni mucho menos.

A continuación te indican las mejores ventajas de Snowflake que tienen tanto atractivo:

1. Arquitectura basada en la nube
Snowflake opera en las nubes, lo que permite a las empresas ampliar y reducir recursos en función de la demanda sin tener de la infraestructura física (hardware). La plataforma cambió se encarga de las tareas rutinarias de mantenimiento, como las actualizaciones de software, la gestión del hardware y el ajuste del rendimiento. Esto alivia la carga de los gases generales de mantenimiento, permiso a las organizaciones centrales en lo que importa: obtener valor de los datos.

2. Elasticidad y escalabilidad
Copo de nieve separa las capas de alojamiento y computación, permitiendo a los usuarios escalar sus recursos informativos independientes de sus necesidades de alojamiento. Esta elasticidad permite gestionar eficazmente diversas cargas de trabajo con un rendimiento óptimo y sin costos innecesarios.

3. Concurrencia y rendimiento
Copo de nieve gestionante la alta concurrencia: varios usuarios pueden acceder a los datos y consultarlos sin pérdida de rendimiento.

4. Compartir datos
Las garantías de seguridad de Snowflake permiten compartir datos con otras organizaciones, departamentos internos, socios externos, clientes u otras partes interesadas. No necesitas completas transferencias de datos.

5. Viaje en el tiempo
Copo de nieve utiliza un término elegante "Viaje en el tiempo" para el versionado de datos. Cada vez que se realiza un cambio en la base de datos, Snowflake toma una instantánea. Esto permite a los usuarios acceder a datos históricos en distintos momentos.

6. Rentabilidad
Copo de nieve de recepción un modelo de pago por uso gracias a su capacidad para escalar los recursos dinámicamente. Sólo pagarás por lo que utilices.

Todas estas ventajas combinadas convenidas a Snowflake en una plataforma en la nube muy deseable para la IA de datos.

Ahora, echemos un vistazo a la arquitectura subyacente de Snowflake que desbloquea estas funciones.

¿Qué es un almacén de datos?
Antes de sumergirnos en la arquitectura de Snowflake, reposemos los almacenes de datos para asegurarnos de que todos estamos en la misma página.

Un almacén de datos es un depósito centralizado que almacena grandes cantidades de datos estructurados y organizados procedimientos de diversas fuentes para una empresa. Diferentes personas (empleados) de las organizaciones utilizan los datos que contienen para obtener diferentes perspectivas.

Por ejemplo, los analistas de datos, en colaboración con el equipo de marketing, pueden realizar una prueba A/B para una nueva campaña de marketing utilizando la tabla de ventas. Los especialistas en RRHH pueden consultar la información de los empleados para hacer un seguimiento de su rendimiento.

Estos son todos de los ejemplos de cómo las empresas de todo el mundo utilizan los almacenes de datos para impulsar el crecimiento. Pero sin una implantación y gestión adeudadas medianas herramientas como Copo de Nieve, los almacenes de datos siguen siendo conceptos elaborados.

Pueden aprender más sobre el tema con nuestro curso de Almacenamiento de Datos.

Arquitectura Copo de Nieve
La arquitectura única de Snowflake, enfermedad para consultas analíticas más rápidas, provisión de su separación de las capas de almacenamiento y computación. Esta distinción contribuye a los beneficios que hemos mencionado antes.

Capa de alojamiento
En Snowflake, la capa de mantenimiento es un componente crítico, que almacena los datos de forma eficiente y escalable. Él adquirió algunas características clave de esta capa:

En la nube: Snowflake se integra perfectamente con los principales probadores de nubes, como AWS, GCP y Microsoft Azure.
Formato columnar: Snowflake alcalena los datos en un formato columnar, optimizado para las consultas analíticas. A diferencia de los formatos tradicionales basados en filas que utilizan herramientas como Postgres, el formato columnar es muy adecuado para la agregación de datos. En el alojamiento columnar, las consultas sólo acceden a las columnas concretas que necesitan, por lo que es más eficiente. Por otra parte, los formatos basados en filas requieren acceder a todas las filas de la memoria para operaciones sencillas como calcular promedios.
Microparticipación: Copo de Nieve utiliza una técnica llamada microparticipación que almacena las tablas en memoria en pequeños trozos. Cada trozo suele ser inmutable y de sólo unos megabytes de tamaño, lo que hace que la optimización y ejecución de las consultas sea mucho más rápida.
Clonación de copia cero: Snowflake tiene una característica única que le permite crear clones virtuales de datos. La clonación es instantánea y no consume memoria adicional hasta que se realizan cambios en la nueva copia.
Escala y elasticidad: La capa de mantenimiento escala horizontalmente, lo que significa que puede manejar volúmenes de datos creados siguiendo más servidores para distribuir la carga. Además, este escalado se produce independientemente de los recursos informativos, lo que es ideal cuando deseas alcanzar grandes volúmenes de datos pero analizar sólo una pequeña fracción.
Veamos ahora la capa de cálculo.

Capa de cálculo
Como su nombre indica, la capa de cálculo es el motor que ejecuta tus consultas. Trabajo conjunto con la capacidad de mantenimiento para procesar los datos y realizar diversas tareas computacionales. Una continuación encuentra más detalles sobre el funcionamiento de esta capa:

Almacenes virtuales: Puedes pensar en los Almacenes Virtuales como equipos de ordenadores (nodos de cálculo) enfermos para gestionar el proceso de consultas. Cada recuerdo del equipo se encarga de una parte diferente de la consulta, lo que hace que la ejecución sea impresionante rápida y paralela. Copo de nieve de recepción Almacenes Virtuales de distintos tonos y, por consiguiente, a distintos precios (los tonos incluyen XS, S, M, L, XL).
Arquitectura multicluster y multinodo: La capa de cálculo utiliza varios clusters con múltiples nodos para una alta concurrencia, permitiendo que varios usuarios accedan a los datos y los consulten simultáneamente.
Optimización automática de consultas: El sistema de Snowflake analiza todas las consultas e identifica patrones para optimizar utilizando datos históricos. Las optimizaciones habituales incluyen la poda de datos innecesarios, el uso de metadatos y la elección de la ruta de ejecución más eficiente.
Caché de resultados: La capa de cálculo incluye una caché que almacena los resultados de las consultas ejecutadas con frecuencia. Cuando se vive a ejecutar la misma consulta, los resultados se desarrollaron casi instantáneamente.
Todos estos principios de enfermedad de la capa de cálculo contribuyen a la capacidad de Snowflake para gestionar cargas de trabajo diferentes y exigentes en la nube.

Capa de servicios en la nube
La última capa son los servicios en la nube. Como esta capa se integra en todos los componentes de la arquitectura de Snowflake, hay muchos detalles sobre su funcionamiento. Además de las funciones relacionadas con otras capas, tiene las responsabilidades adicionales:

Seguridad y control de acceso: Esta capa aplica medidas de seguridad, como la autenticación, la autorización y la cifrado. Los administradores utilizan el Control de Acceso Basado en Funciones (RBAC) para definir y gestionar las funciones y permisos de los usuarios.
Compartir datos: Esta capa implementa protocolos seguros de intercambio de datos entre diferentes cuentas e incluso organizaciones de terceros. Los consumidores de datos pueden acceder a ellos sin necesidad de movimientos, lo que fomenta la colaboración y la monetización de los datos.
Soporte de datos semiestructurados: Otra venta exclusiva de Snowflake es su capacidad para manejar datos semiestructurados, como JSON y Parquet, a pesar de ser una plataforma de gestión de almacenes de datos. Puede consultar facilmente datos semiestructurados e integrar los resultados con las tablas existentes. Esta flexibilidad no se ve en otras herencias RDBMS.
Ahora que tenemos una imagen de alto nivel de la arquitectura de Snowflake, vamos a escribir algo de SQL en la plataforma.

Configurar Snowflake SQL
Snowflake tiene su propia versión de SQL llamada Snowflake SQL. La diferencia entre este y otros dialectos de SQL es similar a la diferencia entre los acentos del inglés.

Muchas de las consultas analíticas que realizan en dialectos como PostgreSQL no cambian, pero hay algunas discrepancias en los comandos DDL (Lenguaje de Definición de Datos).

Ahora, ¡vamos a ver codo ejecutar algunas consultas!

Snowsight: Interfaz web
imagen3.png

Para empezar a utilizar Snowsight, ve a la página de prueba gratuita de 120 días de Snowflake y crea una cuenta. Presentar tus datos personales y seleccionar cual probar de nube de la lista. Esto proporciona una prueba gratuita de 120 días en lugar de la prueba más estar de 30 días que puedes encontrar en otros sitios. La compra también incluye créditos por valor de 400 $. 

Al inscribir para una prueba, se recomienda que los usuarios elijan AWS y la región Oeste de EEUU-Oregón. Entre otras razones, Oregón es una de las regiones con costos más bajos para la infraestructura de AWS y, en consecuencia, los créditos de prueba duran más.

Tras verificar tu correo electrónico, será redirigido a la página Hojas de trabajo. Las hojas de trabajo son entornos interactivos de codificación en vivo en los que podemos escribir, ejecutar y ver los resultados de tus consultas SQL.

imagen8.png

Para realizar armas consultas, necesitamos una base de datos y una tabla (no utilizaremos los datos de muerte de Snowsight). Para empezar, te sugiero que intenciones crear una nueva base de datos (podrías llamada algo así comotest_db) y una tabla con el nombre de un archivo CSV local. Puedes descargar el archivo CSV ejecutando el código de este gist de GitHub en tu terminal.

Despuestas, se te dirigirá a una nueva hoja de cálculo donde podrás echar cual cual consulta SQL que desees. La interfaz de la hoja de cálculo me parece bastante sencilla y muy funcional. Tómate unos minutos para familiarizarte con los paneles, los botones y sus respetivas ubicaciones.

Conclusión y aprendizaje posterior
¡Uf! Empezamos con otros conceptos sencillos, pero hacia el final, nos metimos de lleno en los detalles escabrosos. Bueno, esa es mi idea de un tutorial decente.

Probablemente habrás adivinado que Snowflake es mucho más de lo que hemos visto. De hecho, ¡la documentación de Snowflake incluye guías de inicio rápido que en realidad duran 128 minutos! Pero antes de abordarlas, te recomiendo que te mojes las manos con otros recursos. ¿Qué te parece estas?

Curso de Introducción a un Copo de Nieve
Un seminario web sobre la modernización de la analítica de ventas con Snowflake
Análisis de datos en Snowflake con código Python
Guías de usuario oficiales de Snowflake
Copo de nieve Northstar para saber más sobre la visión a largo espacio de Copo de nieve.
¡Gracias por leer!