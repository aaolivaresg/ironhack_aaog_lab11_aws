## Resource Management Strategy

Para que la aplicación de E-commerce funcione de manera eficiente y controlada, usaremos herramientas que aseguren que siempre haya suficientes recursos para atender a los clientes sin gastar más de lo necesario.

### Auto Scaling:

Es un sistema que ajusta automáticamente la cantidad de servidores (o instancias) según el tráfico que reciba la aplicación. Si hay más usuarios, se añaden más servidores; si el tráfico baja, se eliminan los servidores sobrantes.

- Mínimo de servidores: Siempre tendremos al menos 2 servidores activos para garantizar que la aplicación esté disponible.
- Máximo de servidores: Limitamos la cantidad para evitar gastos innecesarios (por ejemplo, 10 servidores en total).
- Reglas automáticas:
Si el tráfico o el uso del servidor suben mucho (por ejemplo, durante el Black Friday), añadimos servidores.

### Load Balancing:

Es un sistema que distribuye el tráfico de los usuarios entre todos los servidores disponibles para que ninguno se sobrecargue y la experiencia sea rápida y confiable.
### Cost Optimization:

Es una herramienta que nos ayuda a controlar cuánto gastamos en los servicios de AWS y nos avisa si estamos gastando más de lo planeado.
Así aseguramos que los costos se mantengan dentro del presupuesto y no haya sorpresas al final del mes.


Estos puntos considero serían los básicos para la definición de una estrategia de gestión de recursos en la aplicación de E-commerce.
