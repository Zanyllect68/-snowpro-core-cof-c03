**1. Arquitectura y Ediciones de Snowflake**
00:00 - 00:04
Bienvenido a este curso sobre la Arquitectura de Snowflake.

**2. Arquitectura Funcional de Snowflake**
00:04 - 00:12
¡Aquí construirás las bases para obtener la certificación SnowPro Core en muy poco tiempo! Comencemos entendiendo cómo está estructurado realmente Snowflake.

**3. El problema con las bases de datos tradicionales**
00:12 - 00:41
Comencemos observando las bases de datos tradicionales; estas estaban estrechamente acopladas, lo que significa que el almacenamiento y el procesamiento (*compute*) funcionaban en el mismo hardware físico. Esto funcionaba bien a pequeña escala, pero cuando los equipos de datos crecían o los analistas ejecutaban múltiples consultas al mismo tiempo, rápidamente te topabas con un límite: no podías simplemente añadir más potencia de procesamiento; tenías que escalar tanto el almacenamiento como el procesamiento a la vez, lo necesitaras o no.

**4. Tres capas: Almacenamiento**
00:41 - 00:58
Snowflake fue fundada en 2012 con un enfoque fundamentalmente diferente: desacoplar estas piezas en tres capas separadas. Primero, la capa de almacenamiento, donde tus conjuntos de datos se comprimen en un formato basado en columnas, en el proveedor de nube que estés utilizando.

**5. Tres capas: Procesamiento (*Compute*)**
00:58 - 01:05
Segundo, la capa de procesamiento, que es donde realmente se ejecutan las consultas, dentro de lo que Snowflake llama *Virtual Warehouses* (almacenes virtuales).

**6. Tres capas: Servicios en la nube**
01:05 - 01:22
Y finalmente, la capa de servicios en la nube. Esta capa coordina todo, desde la autenticación hasta la gestión de metadatos, optimización de consultas y control transaccional, todo esto antes de que una consulta siquiera toque la capa de procesamiento. Cada capa se comunica con las demás. Ninguna está bloqueada entre sí.

**7. Almacenamiento y Procesamiento**
01:22 - 01:53
Cuando usas Snowflake por primera vez, puede resultar contraintuitivo porque el almacenamiento y el procesamiento se facturan por separado. Tus datos siempre están ahí, con una tarifa de almacenamiento fija y continua, pero el procesamiento solo te cuesta cuando realmente se está realizando trabajo. Un *virtual warehouse* que está inactivo no te cuesta nada en procesamiento. Eso cambia la forma en que piensas sobre la asignación de recursos, porque puedes encender un *warehouse* dedicado para un trabajo puntual, dejar que se suspenda cuando termine, y ahí termina el costo.

**8. Capa de almacenamiento compartido**
01:53 - 02:25
Piénsalo de esta manera: una capa de almacenamiento en el centro con tres *warehouses* separados conectados a ella: uno para el equipo de ingeniería, otro para el equipo de producto y otro para las cargas de trabajo del equipo de marketing. Los mismos datos, pero sin compartir el procesamiento. Esto significa que si el equipo de marketing inicia una exportación grande, el equipo de ingeniería no lo nota. El aislamiento de cargas de trabajo es una de las razones principales por las que las organizaciones eligen Snowflake sobre las arquitecturas tradicionales.

**9. Ediciones de Snowflake**
02:25 - 03:21
Ahora entremos en las Ediciones de Snowflake. Snowflake ofrece cuatro tipos, pero las más utilizadas y a las que se hace referencia principalmente en este curso son *Standard* y *Enterprise*. *Standard* es adecuada para la mayoría de los equipos que están empezando, como una *startup* que ejecuta analítica interna, por ejemplo. *Enterprise* es donde suelen aterrizar las organizaciones en crecimiento, como un negocio minorista que realiza informes para múltiples equipos con necesidades de retención de datos más largas. Snowflake también ofrece una edición *Business Critical*, enfocada en el cumplimiento normativo; piensa en registros de pacientes, datos financieros o cualquier cosa con un requisito regulatorio. También ofrecen *Virtual Private Snowflake*, que proporciona una infraestructura totalmente dedicada; piensa en agencias gubernamentales o contratistas de defensa donde los recursos compartidos no son una opción. Esta tabla tiene el desglose completo de características.

**10. Cobertura global**
03:21 - 03:39
Por último, Snowflake funciona en los tres principales proveedores de nube: AWS, Azure y Google Cloud, los cuales pueden desplegarse en regiones de todo el mundo. Tu cuenta vive en un proveedor y en una región, pero la plataforma en sí es independiente de la nube (*cloud-agnostic*).

**11. Prepárate para la certificación SnowPro Core**
03:39 - 04:24
Antes de terminar, yo, Emily, desarrolladora de currículo técnico en Snowflake, quisiera ofrecerte unas palabras sobre cómo este curso encaja en el panorama general. Este es el primer curso de la ruta de Certificación SnowPro Core en DataCamp, y se alinea con la insignia *Snowflake University Platform Skills*. Es también el primero de tres cursos en una serie destinada a prepararte para la certificación SnowPro Core. No estamos empezando desde cero: ya deberías sentirte cómodo con conceptos cotidianos de Snowflake y con escribir SQL. Si eres completamente nuevo en estos conceptos, te recomendamos que primero tomes nuestros cursos de SQL introductorio y de Snowflake, como "Introducción a Snowflake".

**12. Certificación SnowPro® Core (COF-C03)**
04:24 - 04:52
Esta ruta ha sido creada en conjunto con Snowflake para ayudarte a aprobar el examen de certificación SnowPro Core. Los cursos cubren las habilidades clave evaluadas en el examen, incluyendo arquitectura de Snowflake, gestión de cuentas, carga de datos, optimización de rendimiento y colaboración. Completa la ruta y gana un código de descuento de $50 por parte de Snowflake para tu examen SnowPro Core; una excelente manera de validar tu experiencia en Snowflake.

**13. ¡Practiquemos!**
04:52 - 05:03
A lo largo de los próximos capítulos, seguiremos construyendo sobre estas bases para prepararte para convertirte en un SnowPro. ¡Pongamos a prueba tu conocimiento sobre la arquitectura de Snowflake!