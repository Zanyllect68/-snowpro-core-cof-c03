1. El mercado de copos de nieve
00:00 - 00:00
Las acciones seguras y las salas limpias se encargan de compartir entre cuentas específicas. The Marketplace lleva esto más allá — es un catálogo donde cualquier cuenta de Snowflake puede descubrir y consumir productos y aplicaciones de datos publicados por proveedores externos, todo sin canalizaciones, transferencias ni salida de Snowflake. Este video cubre cómo funcionan los listados, cómo consumirlos y publicarlos, y en qué se diferencian los listados de aplicaciones nativas de los listados de datos.

2. ¿Qué es el Mercado de Copos de Nieve?
00:00 - 00:00
Snowflake Marketplace es un catálogo público de productos y aplicaciones de datos, al que se puede acceder directamente desde Snowsight — sin cuentas externas, sin claves API, sin suscripciones separadas. Los listados de datos utilizan el mismo mecanismo de intercambio subyacente que el intercambio seguro de datos. La diferencia es la capacidad de descubrimiento: en lugar de una participación privada entre dos cuentas conocidas, los listados de Marketplace están disponibles para cualquier cuenta de Snowflake. Para Claro, aquí es donde el equipo de ciencia de datos encuentra indicadores macroeconómicos, índices de precios inmobiliarios o datos demográficos para enriquecer los modelos de riesgo crediticio.

3. Listados de datos
00:00 - 00:00
Los listados de datos vienen en dos tipos. Los listados gratuitos están disponibles de inmediato — el consumidor hace clic en Obtener y aparece una base de datos compartida en su cuenta, sin necesidad de aprobación, pago o canalización. Los listados pagos requieren una suscripción o un acuerdo de uso. Una vez aprobados los términos, se aplica el mismo proceso de montaje. En ambos casos, los datos aparecen como una base de datos compartida que el consumidor puede consultar directamente. Cuando el proveedor actualiza su conjunto de datos, el consumidor ve la actualización inmediatamente en su próxima consulta.

4. Consumir un listado
00:00 - 00:00
Consumir un listado de Marketplace es deliberadamente sencillo. En Snowsight, navegue por Marketplace, busque el listado y haga clic en Obtener. Snowflake crea una base de datos compartida en la cuenta del consumidor. Opcionalmente, los consumidores pueden especificar un nombre para esa base de datos y pueden otorgar acceso a ella utilizando declaraciones GRANT estándar. A partir de ese momento lo consultan con SQL estándar. Sin ETL, sin actualización programada, sin canalización que mantener. En Claro, agregar un conjunto de datos de indicadores macroeconómicos para enriquecer los modelos crediticios es un proceso de tres pasos: encontrarlo, montarlo, unirse a él.

5. Publicar un listado como proveedor
00:00 - 00:00
Cualquier cuenta de Snowflake puede publicar un listado después de completar el registro del proveedor. El proceso refleja la creación de un recurso compartido privado: define qué bases de datos y objetos incluir y luego configura la visibilidad y los precios del listado. Un listado puede ser público para cualquier cuenta de Snowflake o estar restringido a un conjunto definido de cuentas para una distribución controlada. En Claro, la publicación de agregados anónimos de tendencias crediticias permitiría a las empresas de investigación financiera suscribirse sin que Claro construya un canal de distribución de datos separado.

6. Listados de datos versus listados de aplicaciones nativas
00:00 - 00:00
El Marketplace también alberga listados de aplicaciones nativas, fundamentalmente diferentes de los listados de datos. Una lista de datos brinda al consumidor acceso de lectura a un conjunto de datos. Una aplicación nativa instala una aplicación directamente en la cuenta Snowflake del consumidor— con su propia interfaz de usuario, procedimientos almacenados, funciones y datos agrupados. El consumidor no sólo consulta datos; interactúa con la aplicación. Un modelo de calificación crediticia empaquetado como una aplicación nativa expondría un procedimiento almacenado que Claro llama con sus propios datos como entrada. La distinción clave aquí es que los listados de datos comparten datos y las aplicaciones nativas comparten funcionalidad.

7. ¡Vamos a practicar!
00:00 - 00:00
Con esto concluimos nuestra mirada al Mercado Snowflake. Ahora es tu turno — vamos a practicar.