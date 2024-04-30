# DaemonSet

Un DaemonSet en Kubernetes es un tipo de controlador de recursos que garantiza que una instancia de un pod (o varias) se ejecute en cada nodo del clúster. Es útil cuando necesitas que ciertos pods se ejecuten en todos los nodos del clúster para realizar tareas específicas, como recopilación de registros, monitoreo, almacenamiento de datos locales, entre otros.

Algunos casos de uso comunes para DaemonSets incluyen:

1. **Recopilación de registros**: Ejecutar un pod en cada nodo para recopilar registros de contenedores y enviarlos a un sistema centralizado de gestión de registros.

2. **Monitoreo y métricas**: Desplegar un pod en cada nodo para recopilar métricas del sistema y del clúster, que luego se envían a un servidor de monitoreo.

3. **Almacenamiento local de datos**: Utilizar un pod en cada nodo para montar almacenamiento local en el nodo y almacenar datos de forma eficiente y rápida.

Un DaemonSet garantiza que, independientemente de la escalabilidad del clúster, siempre habrá una instancia de los pods asociados ejecutándose en cada nodo. Esto lo hace ideal para tareas que requieren presencia en todos los nodos del clúster.