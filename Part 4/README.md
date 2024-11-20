## Theoretical Implementation


Para poder ilustrar este paso creo que es necesario definir un happy path para el flujo de la aplicación. De esta forma, podremos identificar los componentes que se necesitan para que la aplicación funcione correctamente y podremos definir los casos de uso que se deben implementar.

#### Un usuario entra a la aplicación, busca productos, realiza un pedido y recibe confirmación.



### 1. Interacción del Usuario con la Aplicación
   Cliente (Frontend):

El usuario accede a la aplicación desde su navegador o dispositivo móvil.
La aplicación frontend está alojada en Amazon S3 (contenido estático como HTML, CSS, JS) y servida a través de Amazon CloudFront para mejorar la velocidad de entrega.
Ejemplo:

El usuario ingresa a www.tiendaonline.com, y CloudFront sirve los archivos directamente desde S3.
Amazon CloudFront:

Actúa como una red de distribución de contenido (CDN), entregando rápidamente los archivos estáticos y optimizando la experiencia del usuario.
Redirige las solicitudes dinámicas (como búsquedas de productos) al backend a través de Application Load Balancer (ALB).

---

### 2. Procesamiento de Solicitudes

#### Application Load Balancer (ALB):

Recibe solicitudes del frontend y las distribuye a las instancias de backend en Amazon EC2.
Gestiona rutas específicas:

- /products -> Microservicio de catálogo.
- /orders -> Microservicio de pedidos.
- /users -> Microservicio de usuarios.

Ejemplo:

El usuario busca un producto, y el ALB redirige la solicitud al microservicio de catálogo.

#### Instancias EC2 (Backend):

Cada microservicio (productos, usuarios, pedidos) opera en instancias EC2 dentro de subredes privadas en Amazon VPC.
Las instancias están configuradas con Auto Scaling, garantizando que siempre haya suficientes servidores para manejar el tráfico.
microservicio de productos recibe una solicitud de búsqueda y consulta los datos en la base de datos.

---

### 3. Almacenamiento y Bases de Datos

#### Amazon RDS (Relational Database Service):

Almacena datos estructurados como:
* Información de usuarios.
* Detalles de productos (nombres, precios, inventario).
* Historial de pedidos.

* Configurado en un entorno multi-AZ para alta disponibilidad.

Ejemplo:

El microservicio de catálogo consulta a RDS para buscar "mesa" y devuelve los resultados al usuario.

#### Amazon S3:

Almacena imágenes de productos, recibos de compra y otros archivos estáticos.
Integra con el backend para que los microservicios puedan cargar o acceder a imágenes.

Ejemplo:

El usuario ve las imágenes de los productos que se cargan desde S3.


---

### 4. Finalización del Pedido
#### Proceso de Pedido:

El usuario añade productos al carrito y confirma el pedido.
El microservicio de pedidos valida la transacción y actualiza el inventario en RDS.

#### Notificaciones con Amazon SNS:

Una vez procesado el pedido, el backend publica un mensaje en Amazon SNS.
SNS envía una notificación al usuario (por correo electrónico o mensaje de texto) confirmando su compra.

Ejemplo:

"Gracias por tu compra. Tu pedido #12345 será enviado."

---

### 5. Seguridad y Red
#### Amazon VPC:

Toda la infraestructura opera dentro de una VPC aislada para mayor seguridad.

#### AWS IAM:

Los roles de IAM aseguran que cada componente solo tenga acceso a los recursos necesarios.

Por ejemplo:
El rol de backend tiene permisos para consultar RDS y cargar imágenes en S3, pero no puede modificar configuraciones del balanceador.
