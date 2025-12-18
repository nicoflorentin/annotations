**Conceptos Clave:**

- **¿Qué es Singleton?** Es un patrón de diseño creacional que asegura que una clase tenga una única instancia (objeto) en toda la aplicación, evitando la creación constante de objetos innecesarios y optimizando el uso de memoria (0:57). Permite un punto de acceso global a esa única instancia desde cualquier parte del programa (1:21).
- **Ejemplo en la vida real:** Se compara con el CEO o presidente de una empresa, donde solo puede haber una persona en ese rol y todas las decisiones finales pasan por ella, sirviendo como un punto de acceso único para todos (1:35).
- **Problema que resuelve:** Evita la inconsistencia de datos, el consumo innecesario de recursos y el acceso a múltiples copias de la misma configuración (por ejemplo, una configuración de base de datos) que tendrían que actualizarse en varios lugares (2:17).

**Implementación en Código (Java):** El patrón Singleton se basa en tres partes fundamentales (4:33):

1. **Constructor privado:** Impide que otras clases creen nuevas instancias directamente usando `new` (4:40).
2. **Variable estática privada:** Contiene la única instancia de la clase. Es `static` para que pertenezca a la clase y no a un objeto, y `private` para controlar el acceso (4:52).
3. **Método público estático (`getInstancia`):** Es el único punto de acceso para obtener la instancia del Singleton. Verifica si la instancia ya existe; si no, la crea por primera vez y luego la devuelve. Si ya existe, simplemente devuelve la instancia existente (5:01).

**Ejemplo práctico:** El video muestra un ejemplo con una clase `Configuración` que simula una configuración de sistema. Se demuestra cómo dos "módulos" diferentes (autenticación y reportes) intentan acceder a la configuración. La primera vez que se solicita la instancia, se crea e inicializa. Las solicitudes posteriores reciben la misma instancia ya existente, sin volver a inicializarla (10:17). La prueba final compara las referencias en memoria de las dos instancias obtenidas, demostrando que son idénticas (`true`), confirmando que ambas apuntan al mismo objeto en memoria (14:52).