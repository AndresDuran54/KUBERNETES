## Comando: Aplicar Configuración de un Pod desde un Archivo YAML

El comando `kubectl apply -f SECCION_6/CREAR_POD_MULTI/multi.yaml` se utiliza en Kubernetes para aplicar la configuración de un pod desde un archivo YAML. Aquí está el desglose del comando:

- `kubectl apply`: Este es el comando base para aplicar configuraciones en Kubernetes. Se utiliza para crear o actualizar recursos en el clúster según la definición proporcionada en un archivo YAML.

- `-f SECCION_6/CREAR_POD_MULTI/multi.yaml`: Con esta opción, estás especificando la ubicación del archivo YAML que contiene la configuración del pod que deseas crear o actualizar. En este caso, el archivo se encuentra en la ruta "SECCION_6/CREAR_POD_MULTI/multi.yaml".

El archivo YAML `multi.yaml` debe contener toda la definición del pod, incluyendo su nombre, contenedores, volúmenes, configuraciones de red y cualquier otro detalle necesario para crear el pod.

En resumen, el comando `kubectl apply -f SECCION_6/CREAR_POD_MULTI/multi.yaml` se utiliza para aplicar la configuración de un pod contenido en el archivo YAML "multi.yaml". Una vez ejecutado el comando, Kubernetes creará o actualizará el pod según lo definido en el archivo YAML.

Este enfoque de declarar la configuración en archivos YAML facilita la gestión y el despliegue de recursos en Kubernetes, ya que puedes versionar y compartir estos archivos para mantener un control preciso sobre el estado de tu clúster.

## Comando: Ver los Logs de un Contenedor en Tiempo Real

El comando `kubectl logs -f multi -c frontal` se utiliza en Kubernetes para ver los registros (logs) generados por un contenedor específico en tiempo real. Aquí está el desglose del comando:

- `kubectl logs`: Este es el comando base para obtener los registros de un contenedor en Kubernetes. Te permite acceder a la salida de los registros generados por un contenedor en un pod.

- `-f`: Esta opción, también conocida como `--follow`, permite seguir los registros en tiempo real. Con esta opción activada, el comando mostrará continuamente los nuevos registros que se generen.

- `multi`: Con esta parte del comando, estás especificando el nombre del pod del cual deseas ver los registros. En este caso, el pod se llama "multi".

- `-c frontal`: Esta opción, o `--container`, indica que quieres ver los registros del contenedor llamado "frontal" dentro del pod. En los pods con múltiples contenedores, esta opción te permite seleccionar el contenedor del cual deseas ver los registros.

En resumen, el comando `kubectl logs -f multi -c frontal` se utiliza para seguir en tiempo real los registros generados por el contenedor "frontal" dentro del pod llamado "multi" en Kubernetes
