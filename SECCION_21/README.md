# Sondas

En Kubernetes, las sondas son mecanismos utilizados para monitorear y gestionar el estado de los contenedores en un pod. Permiten al sistema de Kubernetes realizar comprobaciones de salud, iniciación y terminación de manera automatizada, lo que garantiza que los contenedores estén en un estado saludable y funcionando correctamente. Existen tres comportamientos principales de sondas en Kubernetes:

1. **Sonda de Liveness (Sondeo de Vida)**:
   - La sonda de liveness se utiliza para verificar si un contenedor está en un estado saludable y operativo. Si la sonda de liveness falla, Kubernetes considerará que el contenedor está en un estado no saludable y puede intentar reiniciarlo automáticamente.
   - Si un contenedor falla la sonda de liveness, Kubernetes intentará reiniciarlo para restaurar su estado saludable.

2. **Sonda de Readiness (Sondeo de Disponibilidad)**:
   - La sonda de readiness se utiliza para determinar si un contenedor está listo para recibir tráfico de red. Si un contenedor no pasa la sonda de readiness, Kubernetes dejará de enviar tráfico de red a ese contenedor hasta que vuelva a estar listo.
   - La sonda de readiness es útil para evitar que los contenedores reciban tráfico antes de que estén completamente inicializados o preparados para manejar solicitudes.

3. **Sonda de Startup (Sondeo de Inicio)**:
   - La sonda de startup es un tipo de sonda de liveness que se utiliza para verificar el estado inicial de un contenedor después de que se ha iniciado.
   - Esta sonda se ejecuta solo una vez después de que el contenedor se ha iniciado y puede ser útil para realizar tareas de inicialización específicas antes de que el contenedor esté completamente operativo.

Estas sondas se configuran en el manifiesto del pod y pueden personalizarse según las necesidades específicas de la aplicación para garantizar su correcto funcionamiento dentro del clúster de Kubernetes.

En Kubernetes, existen tres tipos principales de sondas que se pueden utilizar para verificar el estado de los contenedores en un pod:

1. **ExecProbe (Sonda de ejecución)**:
   - Esta sonda ejecuta un comando dentro del contenedor y verifica el resultado para determinar si el contenedor está en un estado saludable.
   - El comando ejecutado puede ser cualquier comando válido dentro del contenedor, como un script de shell, un programa específico, etc.
   - Si el comando se ejecuta exitosamente (devuelve un código de salida 0), la sonda se considera exitosa.
   
2. **HTTPProbe (Sonda HTTP)**:
   - Esta sonda envía una solicitud HTTP a un endpoint específico dentro del contenedor y verifica la respuesta para determinar si el contenedor está en un estado saludable.
   - Se utiliza comúnmente para sondas de servicios web y aplicaciones que pueden responder a solicitudes HTTP.
   - Si la respuesta HTTP indica que el servicio está disponible (por ejemplo, un código de estado 200), la sonda se considera exitosa.

3. **TCPSocketProbe (Sonda de socket TCP)**:
   - Esta sonda establece una conexión TCP con un puerto específico dentro del contenedor y verifica si la conexión se puede establecer correctamente.
   - Se utiliza para verificar la disponibilidad de servicios que no utilizan HTTP, como bases de datos o servidores de aplicaciones que exponen un puerto TCP.
   - Si la conexión TCP se establece correctamente, la sonda se considera exitosa.

Estos tipos de sondas proporcionan flexibilidad para verificar diferentes aspectos del estado de un contenedor, dependiendo de las necesidades específicas de la aplicación. Pueden combinarse con los comportamientos de sonda mencionados anteriormente para definir cómo se manejan las respuestas de las sondas y cómo afectan al estado de los pods en Kubernetes.