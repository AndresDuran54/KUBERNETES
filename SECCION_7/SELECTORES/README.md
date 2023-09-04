# Selectores en Kubernetes

## Comando: Listar Pods con Etiquetas Excluyendo Valores Específicos

El comando `kubectl get pods --show-labels -l 'estado notin (desarrollo,testing)'` se utiliza para obtener una lista de todos los pods que no tienen la etiqueta "estado" establecida en "desarrollo" o en "testing" en Kubernetes. Aquí está el desglose del comando:

- `kubectl get pods`: Esta parte del comando indica que deseas obtener información sobre los pods en el clúster Kubernetes.

- `--show-labels`: Con esta opción, estás solicitando que se muestren las etiquetas asociadas a los pods en la salida. Esto te permitirá ver las etiquetas de cada pod en la lista.

- `-l 'estado notin (desarrollo,testing)'`: Aquí estás utilizando la opción `-l` o `--selector` para especificar un conjunto de etiquetas y sus valores. Estás buscando los pods que no tienen la etiqueta "estado" establecida en "desarrollo" ni en "testing". El operador `notin` se utiliza para excluir valores específicos.

El comando mostrará una lista de pods que cumplen con estos criterios de etiquetas. Esto puede ser útil para identificar y gestionar pods que no están en los estados de "desarrollo" ni "testing".

## Comando: Eliminar Pods con una Etiqueta Específica en Kubernetes

El comando `kubectl delete pods -l estado=desarrollo` se utiliza en Kubernetes para eliminar todos los pods que tienen la etiqueta "estado" establecida en "desarrollo". Aquí está el desglose del comando:

- `kubectl delete pods`: Esta parte del comando indica que deseas eliminar pods en el clúster Kubernetes.

- `-l estado=desarrollo`: Con esta parte del comando, estás especificando que deseas eliminar todos los pods que tienen la etiqueta "estado" establecida en "desarrollo".

Este comando eliminará todos los pods que coincidan con esta etiqueta específica. Ten en cuenta que la eliminación de un pod es irreversible y todos los datos dentro de ese pod se perderán. Asegúrate de ejecutarlo con precaución y solo cuando sea necesario.
