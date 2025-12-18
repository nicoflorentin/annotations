### Flujo Típico de Autenticación

El proceso de autenticación comienza cuando un usuario ingresa sus credenciales en un **frontend** (por ejemplo, un formulario). Esta información se envía a un **servidor**, que a su vez la valida con una **base de datos** (3:16). Las contraseñas en la base de datos se guardan **encriptadas** (3:54), no en texto plano, lo que explica por qué se deben resetear y no recuperar. Si los datos son correctos, el servidor responde al cliente con información relevante (4:36), excluyendo la contraseña (5:04). La autenticación determina **quién es el usuario** (2:37), no qué puede hacer (para eso está la autorización, que no se cubre en este video) (2:54).

### Métodos de Autenticación

1. **Basic Authentication (5:39)**
    - **Funcionamiento:** El usuario ingresa un correo y una contraseña (5:48). Estos datos se **concatenan** y se codifican utilizando una función **Base64** (5:57). Este string codificado se envía desde el cliente al servidor (6:23). El servidor lo **descifra** (6:31) para obtener el correo y la contraseña, los valida con la base de datos y permite el acceso (6:41). Este proceso se repite en cada petición (13:16).
    - **Ejemplo:** En un navegador, se vería una ventana emergente pidiendo usuario y contraseña para un dominio (6:57).
    - **Ventajas:** Es un método **muy simple** de implementar (7:24).
    - **Desventajas:** Es **altamente inseguro** por sí mismo ya que es reversible y los datos se descifran fácilmente (7:34). Se mejora si se usa sobre HTTPS (7:42), pero generalmente hay mejores alternativas.

2. **Autenticación basada en Tokens (7:51)**    
    - **Funcionamiento:** Un usuario ingresa sus credenciales (7:58), el servidor las valida con la base de datos (8:06). Si son correctas, el servidor **genera un token** (8:16), que es un string largo (8:20), típicamente un **JSON Web Token (JWT)** (15:17). Este token se genera con información del usuario (ID, nombre, correo, etc.), un algoritmo y un "secret" que solo conoce el servidor (9:46).
    - El servidor envía este token al cliente (10:23), que lo **guarda** (10:27) (comúnmente en **cookies** o **local storage** del navegador) (11:23). En cada petición futura, el cliente envía este token en la cabecera `Authorization` con el prefijo `Bearer` (14:29). El servidor valida el token y responde.
    - **Ventajas:** El token es una credencial que se guarda y se envía en cada petición, actuando como un carnet de identidad (10:54). Es el **estándar actual** en muchos sistemas (15:32).
    - **Desventajas de un solo token:** Si alguien copia el token, puede usar la cuenta (16:30). No se puede invalidar fácilmente hasta que expire (16:42).
    - **Mejora: Access Tokens y Refresh Tokens (17:33)**
        - **Access Token:** Tiene una **duración corta** (minutos u horas) (17:49). Se usa para peticiones diarias. Cuando expira, el servidor devuelve un error 403 (18:05).
        - **Refresh Token:** Tiene una **duración más larga** (por ejemplo, semanas) (19:40). Cuando el Access Token expira, el cliente envía el Refresh Token al servidor (18:13) a una ruta especial (por ejemplo, `/refresh`) (18:22). El servidor genera un **nuevo Access Token y un nuevo Refresh Token** (18:32), invalidando el anterior.
        - Los Refresh Tokens se almacenan en una base de datos (por ejemplo, Redis) (19:16) para mantener un registro y poder **invalidarlos** (19:56) (cerrar sesión) (20:34).

3. **OAuth2 (21:11)**
    - **Funcionamiento:** Permite iniciar sesión con servicios de terceros como **Google o Facebook** (21:17). El usuario hace clic en el botón de login, el cliente envía una petición al servidor del proveedor (21:22). Después de la autorización del usuario en el proveedor (21:35), el servidor del proveedor (ej. Google) envía un **código** (no un token) (21:55) al servidor de la aplicación (en una URL de callback) (21:43).
    - El servidor de la aplicación usa este código para hacer una nueva petición al proveedor, enviando datos de la aplicación (`client ID`, `client Secret`, el código, etc.) (22:12). El proveedor responde con un **Access Token y un Refresh Token** (22:37).
    - Con estos tokens, la aplicación puede solicitar información del usuario (correo, nombre, foto de perfil) al proveedor (22:57).
    - **Ventajas:** El usuario no comparte sus credenciales directamente con la aplicación (23:28). El usuario puede **revocar el acceso** de la aplicación en cualquier momento desde el proveedor (23:36).

4. **Single Sign-On (SSO) y Protocolos de Identidad (23:53)**
    - **Funcionamiento:** Permite que un usuario se autentique **una sola vez** en una aplicación y acceda a **múltiples servicios relacionados** sin necesidad de volver a iniciar sesión (23:59). Por ejemplo, iniciar sesión en Gmail y automáticamente estar autenticado en Google Drive o Calendar (24:07).
    - Se basa en el protocolo **OAuth2** (24:29) y utiliza un **Identity Provider (IDP)** (24:41), que actúa como validador de los tokens entre las aplicaciones.
    - **Uso:** Común en aplicaciones empresariales (ESRPs como Salesforce) o herramientas internas de compañías (25:22), a menudo utilizando XML (CML) en sistemas antiguos (25:15.