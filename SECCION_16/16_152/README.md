## Comando: Asignar una Etiqueta a un Nodo en Kubernetes

El comando `kubectl label node worker-01 entorno=desarrollo` se utiliza en Kubernetes para asignar una etiqueta al nodo con el nombre `worker-01`, indicando que pertenece al entorno de desarrollo. Aquí está el desglose del comando:

- `kubectl label`: Esta parte del comando indica que se está etiquetando un recurso en Kubernetes.

- `node worker-01`: Especifica que se está etiquetando un nodo específico llamado `worker-01`.

- `entorno=desarrollo`: Esta es la etiqueta que se asigna al nodo. En este caso, se etiqueta el nodo como perteneciente al entorno de desarrollo.

El comando asignará la etiqueta `entorno=desarrollo` al nodo llamado `worker-01`, lo que permitirá identificar y filtrar los nodos según el entorno al que pertenecen.

Recuerda que las etiquetas son metadatos clave-valor que se pueden adjuntar a los recursos de Kubernetes, lo que facilita la organización, búsqueda y gestión de los recursos en el clúster.
