# Documentación de los deployments

## Comando: Crear un Despliegue en Kubernetes

El comando `kubectl create deployment apache --image=http` se utiliza en Kubernetes para crear un nuevo despliegue en el clúster. Un despliegue es un objeto que administra la implementación de aplicaciones en Kubernetes, asegurando que el número especificado de réplicas de la aplicación esté en funcionamiento en todo momento.

**Descripción:**

- `apache`: Este es el nombre que asignamos al nuevo despliegue. Puedes cambiarlo según tus preferencias.

- `--image=http`: Aquí se especifica la imagen que se utilizará para implementar la aplicación en el despliegue.

**Ejemplo:**

Para crear un despliegue utilizando una imagen válida de Docker, puedes usar un comando similar al siguiente:

```sh
kubectl create deployment apache --image=httpd
``````

## Comando: Aplicar un Archivo de Despliegue en Kubernetes

El siguiente comando se utiliza en Kubernetes para aplicar la configuración de un despliegue utilizando un archivo YAML. En este caso, se está aplicando la configuración del despliegue desde el archivo "deployment.yaml" ubicado en la ruta "SECCION_8/DEPLOYMENTS/". Asegúrate de que el archivo YAML contenga la configuración del despliegue que deseas aplicar.

```sh
kubectl apply -f SECCION_8/DEPLOYMENTS/deployment.yaml
```
**Descripción:**

Este comando aplicará la configuración del despliegue definida en el archivo YAML al clúster de Kubernetes. El despliegue se encargará de implementar y administrar la aplicación de acuerdo con la configuración especificada en el archivo.

Recuerda ajustar la ruta del archivo y el nombre del archivo YAML según tu estructura de directorios y el nombre real del archivo que deseas aplicar.


## Comando: Obtener Despliegues, Pods y Conjuntos de Réplicas con Etiqueta "app=nginx"

El siguiente comando se utiliza en Kubernetes para obtener información sobre despliegues (Deployments), pods y conjuntos de réplicas (ReplicaSets) que tengan la etiqueta "app=nginx". El uso de la opción `-l` permite filtrar los recursos basados en etiquetas.

```sh
kubectl get deploy,pods,rs -l app=nginx -L app
``````

**Descripción:**

- `kubectl get deploy,pods,rs`: Este comando solicita información sobre despliegues, pods y conjuntos de réplicas en el clúster de Kubernetes.

- `-l app=nginx`: Esta parte del comando especifica el filtro de etiqueta. Solo se mostrarán los recursos que tengan la etiqueta "app=nginx".

- `-L app`: La opción -L o --label-columns se utiliza para especificar qué etiquetas se deben mostrar como columnas adicionales en la salida. En este caso, se mostrará la etiqueta "app" como una columna adicional.

El comando mostrará una lista de despliegues, pods y conjuntos de réplicas que coincidan con la etiqueta "app=nginx", y también mostrará la etiqueta "app" como una columna adicional en la salida.

## Comando: Editar un Despliegue en Kubernetes

El siguiente comando se utiliza en Kubernetes para editar la configuración de un despliegue existente. En este caso, se está editando el despliegue con el nombre "nginx-d".

```sh
kubectl edit deploy nginx-d
```

**Descripción:**

- `nginx-d`: Este es el nombre del despliegue que deseas editar. Al ejecutar este comando, se abrirá un editor de texto en el que podrás modificar la configuración del despliegue.
El comando kubectl edit te permite modificar la configuración de un despliegue directamente en el clúster de Kubernetes. Se abrirá un editor de texto, generalmente el que tengas configurado en tu sistema, con la configuración actual del despliegue. Puedes realizar los cambios necesarios y guardar la configuración para que se apliquen en el clúster.

Asegúrate de tener cuidado al editar la configuración, ya que los cambios pueden afectar el comportamiento del despliegue y, por lo tanto, de la aplicación.

## Comando: Obtener la Configuración de un Despliegue en YAML

El comando `kubectl get deploy nginx-d -o yaml` se utiliza en Kubernetes para obtener la configuración de un despliegue (Deployment) específico llamado "nginx-d" en formato YAML.

**Descripción:**

- `kubectl get deploy nginx-d`: Esta parte del comando indica que deseas obtener información sobre el despliegue específico llamado "nginx-d".

- `-o yaml`: Con esta parte del comando, estás utilizando la opción `-o` o `--output` para especificar el formato de salida. En este caso, estás solicitando que la información se muestre en formato YAML.

El comando mostrará la configuración detallada del despliegue "nginx-d" en un formato YAML. Esto incluirá detalles como las réplicas deseadas, la imagen utilizada y otras configuraciones relacionadas con el despliegue.

Este formato YAML es útil si deseas inspeccionar o modificar la configuración del despliegue de manera programática o realizar un seguimiento detallado de la configuración actual.

Si tienes más preguntas o necesitas más información, no dudes en preguntar.

## Comando: Escalar un Despliegue en Kubernetes

El comando `kubectl scale deploy nginx-d --replicas=10` se utiliza en Kubernetes para ajustar el número de réplicas de un despliegue (Deployment) específico llamado "nginx-d". En este caso, se está escalando el despliegue para tener un total de 10 réplicas.

**Descripción:**

- `kubectl scale deploy nginx-d`: Esta parte del comando indica que deseas escalar el despliegue específico llamado "nginx-d".

- `--replicas=10`: Con esta parte del comando, estás especificando el nuevo número deseado de réplicas para el despliegue. En este caso, se están configurando 10 réplicas.

El comando ajustará automáticamente el número de réplicas del despliegue "nginx-d" a 10. Esto significa que se crearán o eliminarán pods según sea necesario para mantener el número deseado de instancias de la aplicación en funcionamiento.

El escalado es una característica importante en Kubernetes que te permite adaptar la capacidad de tu aplicación según las demandas de carga. Puedes aumentar o reducir el número de réplicas de manera dinámica para garantizar la disponibilidad y el rendimiento de la aplicación.

## Comando: Escalar Despliegues con Etiqueta en Kubernetes

El comando `kubectl scale deploy -l app=nginx --replicas=2` se utiliza en Kubernetes para escalar despliegues que tengan la etiqueta "app=nginx". En este caso, se está escalando todos los despliegues que coincidan con esta etiqueta para tener un total de 2 réplicas cada uno.

**Descripción:**

- `kubectl scale deploy -l app=nginx`: Esta parte del comando indica que deseas escalar todos los despliegues que tengan la etiqueta "app=nginx".

- `--replicas=2`: Con esta parte del comando, estás especificando el nuevo número deseado de réplicas para cada uno de los despliegues seleccionados. En este caso, se están configurando 2 réplicas para cada despliegue con la etiqueta "app=nginx".

El comando ajustará automáticamente el número de réplicas de todos los despliegues que coincidan con la etiqueta "app=nginx" a 2. Esto significa que se crearán o eliminarán pods según sea necesario para mantener el número deseado de instancias de la aplicación en funcionamiento en cada despliegue.

El escalado basado en etiquetas te permite afectar selectivamente grupos de despliegues que compartan una etiqueta común, lo que facilita la gestión de múltiples recursos relacionados.
