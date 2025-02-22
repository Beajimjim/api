# API Modular de Clientes y Pedidos

Este proyecto implementa una API modular para la inserción de clientes y la consulta de pedidos. La estructura se compone de varios archivos que se encargan de recibir solicitudes, procesarlas y conectar a la base de datos, todo de forma escalable y fácil de mantener.

## Descripción del Proyecto

La API cuenta con un punto de entrada central que recibe todas las peticiones y, mediante un parámetro en la URL, dirige la operación solicitada al módulo correspondiente. Entre las funcionalidades principales se encuentran:

- Inserción de clientes en la base de datos.
- Consulta de pedidos.
- Gestión centralizada de errores.
- Obtención de la dirección IP del usuario.
- Interfaz de prueba mediante un formulario HTML.
- Configuración de seguridad y redirecciones a través de un archivo de configuración del servidor.

## Estructura del Proyecto

A continuación se describe la función de cada archivo principal:

### `api.php`

Actúa como controlador frontal de la API. Recibe todas las solicitudes y utiliza el parámetro de la URL (por ejemplo, `o=insertarCliente`) para determinar qué operación ejecutar. Dependiendo del valor del parámetro, se incluye y ejecuta el módulo correspondiente.

### `insertarcliente.php`

Se encarga de procesar la solicitud para insertar un nuevo cliente en la base de datos. Entre sus funciones se encuentran:

- Conexión a la base de datos utilizando MySQLi.
- Extracción de datos enviados mediante `POST` (como nombre, apellidos y clave).
- Ejecución de la consulta SQL para insertar un registro en la tabla correspondiente.
- Manejo de errores durante el proceso de inserción.

### `error.php`

Gestiona y presenta de forma controlada los errores que se produzcan en la API. Su función es mostrar mensajes de error sin exponer detalles sensibles sobre la estructura interna del sistema.

### `ip.php`

Obtiene la dirección IP del usuario que realiza la solicitud. Normalmente utiliza variables del servidor (por ejemplo, `$_SERVER['REMOTE_ADDR']`) para capturar esta información, lo que resulta útil para auditorías y controles de acceso.

### `damepedidos.php`

Recupera y muestra información sobre los pedidos almacenados en la base de datos. La presentación de los datos puede ser en formato HTML o JSON, permitiendo que la información se integre en diferentes interfaces.

### `formulariosimulacro.html`

Proporciona una interfaz de prueba en forma de formulario HTML. Permite al usuario enviar datos a la API, incluyendo campos para `nombre`, `apellidos` y una `clave` predefinida. Al enviar el formulario, se realiza una solicitud `POST` a `api.php` con el parámetro `o=insertarCliente`.

### `.htaccess`

Contiene las directivas de configuración del servidor Apache. Este archivo define reglas de redirección, restricciones de acceso y medidas de seguridad que protegen el sistema y aseguran el correcto funcionamiento de la API.

## Flujo de Ejecución

1. El usuario ingresa datos en el formulario (`formulariosimulacro.html`) y lo envía.
2. La solicitud `POST` se dirige a `api.php` con el parámetro `o=insertarCliente`.
3. `api.php` analiza el parámetro y delega la operación a `insertarcliente.php`.
4. `insertarcliente.php` conecta a la base de datos, extrae los datos enviados y ejecuta la inserción en la tabla correspondiente.
5. En caso de error, `error.php` gestiona y muestra un mensaje adecuado.
6. Archivos adicionales, como `ip.php` y `damepedidos.php`, ofrecen funcionalidades complementarias para obtener la dirección IP del usuario y consultar pedidos, respectivamente.

## Consideraciones

- Verifica que la tabla de la base de datos utilizada para insertar clientes exista y tenga la estructura correcta.
- Asegúrate de que las credenciales y la configuración de la conexión a la base de datos sean las adecuadas.
- Revisa el archivo `.htaccess` para confirmar que las reglas de seguridad y redirecciones están configuradas según las necesidades del proyecto.

