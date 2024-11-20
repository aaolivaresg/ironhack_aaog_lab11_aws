## IAM Configuration

### Dev rol:

Razón: Este rol es indispensable para los programadores que trabajan en la aplicación.
Permisos: Acceso a entornos de desarrollo y qa, y permisos de lectura limitada en producción.

### Admin rol:

Razón: Necesitas un rol con acceso completo para gestionar toda la infraestructura y responder a problemas críticos.
Permisos: Acceso total (aunque idealmente asignado a un número limitado de personas).

### App users rol:

Razón: La aplicación necesita permisos para interactuar con recursos como bases de datos, almacenamiento (S3) y servicios de notificaciones.
Permisos: Acceso controlado a recursos específicos (S3, RDS/DynamoDB, SNS/SQS, etc.).
