1. Protección de datos y continuidad del negocio
00:00 - 00:21
Anteriormente hemos cubierto viajes en el tiempo, seguridad contra fallos y clonación sin copia. Este video profundiza en ellas como herramientas operativas, luego se centra en los grupos de replicación y conmutación por error — los mecanismos de Snowflake para mantener la coherencia de los datos entre cuentas y regiones, y para mantener Claro en funcionamiento si una región deja de funcionar.

2. El problema de la continuidad del negocio
00:21 - 00:49
La protección de datos cubre un espectro de riesgos. Un analista borra registros accidentalmente: Time Travel se encarga de eso. Una región de la nube experimenta una interrupción y la cuenta de Claro deja de estar disponible: los grupos de conmutación por error se encargan de eso. Los usuarios de Claro en la UE necesitan datos que sólo existen en una cuenta estadounidense: la replicación se encarga de ello. Las herramientas son diferentes porque los riesgos son diferentes.

3. Viajes en el tiempo y seguridad contra fallos
00:49 - 01:25
Time Travel le permite consultar o restaurar datos utilizando la sintaxis AT o BEFORE con una marca de tiempo, desplazamiento, ID de declaración o flujo. La profundidad de la ventana depende de tu edición — Ofertas estándar un día, Enterprise hasta noventa. La ventana es configurable por objeto. Beyond Time Travel se encuentra en Fail-Safe: el margen de siete días después del cierre de la ventana de viajes en el tiempo. Fail-Safe no es autoservicio — te comunicas con el soporte de Snowflake y la recuperación es el mejor esfuerzo, no un SLA garantizado.

4. Clonación sin copia: patrones operativos
01:25 - 01:59
Antes de cualquier operación que pueda salir mal, clónala. Antes de que el equipo de Claro ejecute una migración masiva en una tabla de producción, primero la clonan — una copia instantánea sin sobrecarga de almacenamiento en el momento de la creación. Si la migración falla, el clon está allí para restaurarlo. Los clones también promueven datos entre entornos sin duplicar los datos subyacentes. Una vez que existe un clon, es completamente independiente — escribe en el clon, no toque la fuente.

1Ma terial de aprendizaje de copos de nieve
5. ¿Qué es la replicación?
01:59 - 02:32
La replicación copia datos a través de los límites de la cuenta. La cuenta principal de Claro en EE. UU. replica bases de datos para apuntar a cuentas en otras regiones o proveedores de la nube. La replicación es asincrónica — el objetivo es casi en tiempo real pero no un espejo en vivo. Para Claro: una copia de recuperación ante desastres en una región separada, cumplimiento de la residencia de datos con los datos de la UE en una cuenta de la UE y rendimiento de lectura mejorado para los equipos regionales que consultan una copia local.

6. Grupos de replicación
02:32 - 03:06
Replication is managed through replication groups — named collections of databases that replicate together. Either all refresh, or none do. Claro's primary US-East account holds two databases bundled into a group. The secondary EU-West account holds read-only replicas. Replication triggers manually with REFRESH or on a defined schedule. Secondary databases are read-only: queryable but not writable.

7. Creating a Replication Group
03:06 - 03:36
On the primary account, create the replication group, specify which databases to include, and define which target accounts can replicate it. On the secondary account, create a replica using AS REPLICA OF, referencing the primary account and group name. Trigger refreshes with the ALTER REPLICATION GROUP REFRESH command. The primary controls what's in the group; the secondary controls when it refreshes.

8. Failover Groups: What They Add
03:36 - 04:11
A failover group builds on replication groups but adds one critical capability: promoting a secondary to primary. In a replication group, the secondary is always read-only. In a failover group, if the primary goes down, the secondary can be promoted — it becomes writable and takes over as source of truth. Failover groups also replicate account objects: users, roles, warehouses, resource monitors, and integrations.

9. Planned Failover and Failover Mechanics
04:11 - 04:52
Hay dos formas de promover una secundaria. Una conmutación por error planificada es cuando el primario aún está disponible. En una operación, dimite y la secundaria asume el papel de primaria. Esta es una transferencia limpia sin pérdida de datos. Una conmutación por error no está planificada: el principal no está disponible, por lo que el secundario se promociona de inmediato. Debido a que la replicación es asincrónica, cualquier cambio después de la última actualización no será secundario. Ese retraso representa una posible pérdida de datos, razón por la cual la frecuencia de actualización es una decisión de diseño clave.

10. ¡Vamos a practicar!
04:52 - 05:00
Ahora es tu turno. Los próximos ejercicios pondrán a prueba su comprensión de la replicación, los grupos de conmutación por error y las herramientas de protección de datos de Snowflake.