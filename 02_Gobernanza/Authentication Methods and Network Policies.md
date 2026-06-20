1. Métodos de autenticación y políticas de red
00:00 - 00:00
Hemos cubierto lo que los usuarios pueden hacer una vez que están dentro de Snowflake. Pero antes de que todo eso importe, hay una pregunta más fundamental: ¿cómo verifica Snowflake que alguien es quien dice ser y cómo controla qué redes pueden llegar a su cuenta? Eso es lo que cubriremos hoy.

2. ¿Qué es la autenticación?
00:00 - 00:00
La autenticación es el proceso de verificar la identidad. Antes de que Snowflake verifique roles o privilegios, primero confirma quién eres. Un nombre de usuario y una contraseña son la forma más conocida, pero no son los únicos. Snowflake admite varios métodos y la elección correcta depende de quién se conecta: un analista humano que inicia sesión en un navegador tiene requisitos diferentes a los de una canalización automatizada que se ejecuta a las 3 a. m.

3. Métodos y marcos de autenticación
00:00 - 00:00
A continuación veremos los métodos y marcos de autenticación. SSO y SAML permiten a las organizaciones empresariales conectar Snowflake a un proveedor de identidad existente como Okta o Microsoft Entra ID, para que los usuarios inicien sesión con las credenciales de su empresa. OAuth resuelve un problema diferente: es cómo herramientas de terceros, como plataformas de BI y herramientas de integración de datos, se conectan a Snowflake en nombre de un usuario, sin que esas herramientas manejen la contraseña del usuario. A continuación, profundizaremos en cada uno con más detalle.

4. Contraseña y MFA
00:00 - 00:00
La autenticación con contraseña es la base: cada usuario de Snowflake tiene un nombre de usuario y una contraseña. Pero las contraseñas por sí solas son vulnerables: si se expusieran las credenciales de Claro, un atacante podría iniciar sesión directamente. La autenticación multifactor agrega una segunda capa. Snowflake admite dos métodos MFA: Passkey, que utiliza autenticación basada en dispositivo, y TOTP, una contraseña de un solo uso basada en el tiempo generada por una aplicación de autenticación. Incluso si la contraseña se ve comprometida, la cuenta permanece protegida. Los administradores pueden aplicar MFA a nivel de cuenta, por lo que no es opcional.

1 [Copo de nieve: métodos MFA](https://docs.snowflake.com/en/user-guide/security-mfa#restricting-which-mfa-methods-are-available)
5. Autenticación de pares de claves
00:00 - 00:00
La autenticación por pares de claves funciona sin contraseña. El servicio genera un par de claves criptográficas: una clave privada que permanece en el cliente y una clave pública registrada en Snowflake en la cuenta del usuario. Cuando se realiza una conexión, Snowflake verifica que el cliente tenga la clave privada correspondiente. No se transmite ninguna contraseña. Esta es la opción correcta para los pipelines automatizados de Claro donde las cuentas de servicio se ejecutan según un cronograma. El SQL aquí asigna una clave pública utilizando el comando ALTER USER.

6. SSO y OAuth
00:00 - 00:00
SSO uses SAML-based single sign-on: Claro's employees log into Snowflake with their existing company credentials. The identity provider handles the verification, and Snowflake trusts the result. Okta and Microsoft Entra ID both provide native Snowflake support for federated authentication. Snowflake also supports most SAML 2.0-compliant identity providers, so any SAML compliant IdP can be configured. OAuth is designed for third-party tools - when a BI platform needs to connect on behalf of a user, OAuth handles the authorization flow without exposing credentials to the tool.

7. What is a Network Policy?
03:15 - 03:54
By default, any IP address can attempt to connect to your Snowflake account. A network policy lets a security administrator restrict access based on request origin -- IP addresses, private endpoints, or host ports. Policies work through network rules: a network rule is a schema-level object that groups related identifiers, and those rules are then added to the policy's allowed or blocked lists. Connections that don't match the allowed list are rejected before authentication even begins. For Claro, even if credentials were stolen, a connection from an unknown IP is blocked outright.

1 [Snowflake: Network Policies](https://docs.snowflake.com/en/user-guide/network-policies)
8. Creating a Network Policy
03:54 - 04:19
El enfoque moderno utiliza reglas de red para agrupar direcciones IP antes de hacer referencia a ellas en la política. CREATE NETWORK RULE define el conjunto permitido, un rango CIDR para la red corporativa de Claro y una IP de oficina remota específica, y una regla separada para direcciones bloqueadas. CREAR POLÍTICA DE RED luego hace referencia a esas reglas por nombre.

9. Aplicación de una política de red
00:00 - 00:00
Una vez creada, la política se aplica a nivel de cuenta con ALTER ACCOUNT, o a nivel de usuario individual con ALTER USER para restricciones más estrictas en cuentas de servicio específicas.

10. Conectividad privada
00:00 - 00:00
Las políticas de red restringen qué IP pueden llegar a Snowflake a través de Internet público. La conectividad privada va más allá al enrutar el tráfico a través de un punto final de red privado, por lo que nunca atraviesa Internet público. Snowflake admite esto a través de AWS PrivateLink, Azure Private Link y Google Cloud Private Service Connect, según su proveedor de nube. Esto suele ser utilizado por organizaciones con estrictos requisitos de residencia o cumplimiento de datos.

11. ¡Vamos a practicar!
00:00 - 00:00
Ahora entiendes cómo Snowflake verifica la identidad y controla el acceso a la red. Pongamos ese conocimiento en práctica.