# Autoescalado

El autoescalado en Kubernetes es una característica que permite ajustar dinámicamente la cantidad de recursos computacionales asignados a los Pods en función de la carga de trabajo y otros criterios predefinidos. Esta capacidad asegura que las aplicaciones mantengan un rendimiento óptimo, ya sea escalando hacia arriba para manejar picos de demanda o escalando hacia abajo para reducir costos durante períodos de baja utilización.

En Kubernetes, existen principalmente dos tipos de autoescalado:

1. **HPA (Horizontal Pod Autoscaler):** Como mencionaste, el HPA ajusta automáticamente el número de réplicas de los Pods en función de las métricas de recursos, como la CPU y la memoria. Aumenta o disminuye el número de Pods para mantener un nivel predefinido de utilización de recursos y garantizar un rendimiento óptimo de la aplicación.

2. **VPA (Vertical Pod Autoscaler):** A diferencia del HPA que escala horizontalmente añadiendo o eliminando Pods, el VPA ajusta verticalmente los recursos de los Pods, es decir, modifica la cantidad de CPU y memoria asignada a cada Pod. Esto se realiza en función de las necesidades de recursos observadas, lo que permite optimizar el rendimiento y la utilización de recursos en cada Pod individualmente.

3. **CA (Cluster Autoscaler):** El CA es responsable de ajustar automáticamente el tamaño del clúster de Kubernetes en función de la demanda de recursos. Cuando se detecta que no hay suficientes nodos para ejecutar las cargas de trabajo, el CA puede escalar automáticamente el clúster, agregando nuevos nodos según sea necesario. Del mismo modo, cuando los recursos no se están utilizando, el CA puede eliminar nodos para reducir costos y optimizar la utilización de recursos.

Cada uno de estos tipos de autoescalado en Kubernetes aborda diferentes aspectos de la escalabilidad y la gestión de recursos, lo que permite a las aplicaciones adaptarse de manera dinámica a las cambiantes condiciones de carga y optimizar su rendimiento y eficiencia.

### Comando para estresar el pod mediante el servicio apache

El comando que proporcionaste inicia un contenedor de BusyBox que realizará solicitudes HTTP repetitivas al servicio "apache" en tu clúster de Kubernetes. Cada solicitud se realizará cada 0.01 segundos.

Aquí hay una explicación paso a paso del comando:

- `kubectl run`: Este comando crea y ejecuta un contenedor en tu clúster de Kubernetes.
- `-i --tty`: Estas opciones proporcionan una interfaz de terminal interactiva para el contenedor.
- `carga`: Es el nombre que le das al recurso del contenedor que estás creando.
- `--rm`: Esta opción indica a Kubernetes que elimine el contenedor una vez que termine su ejecución.
- `--image=busybox:1.28`: Especifica la imagen de Docker que se utilizará para crear el contenedor. En este caso, estás utilizando la imagen de BusyBox versión 1.28.
- `--restart=Never`: Indica que este contenedor no se reiniciará automáticamente.
- `-- /bin/sh -c "while sleep 0.01; do wget -q -O- http://apache; done"`: Esta es la parte principal del comando que se ejecutará dentro del contenedor. Básicamente, ejecuta un bucle infinito que realiza una solicitud HTTP al servicio "apache" cada 0.01 segundos utilizando el comando `wget`. La opción `-q` de `wget` significa "modo silencioso", lo que significa que no se imprimirá nada en la terminal del contenedor.

Este comando puede ser útil para probar la capacidad de respuesta y la carga de un servicio en tu clúster de Kubernetes. Sin embargo, ten en cuenta que generar una carga pesada de esta manera puede afectar el rendimiento del clúster y de los servicios que se están ejecutando en él. Asegúrate de utilizarlo con precaución y en entornos de prueba adecuados.

### Comando para autoescalar horizontalmente los pods

```bash
kubectl autoscale deployment apache --cpu-percent=40 --min=1 --max=8
kubectl autoscale deployment apache --memory-percent=50 --min=1 --max=5
```

El comando que proporcionaste es para crear un HPA (Horizontal Pod Autoscaler) en Kubernetes. Este comando escalará automáticamente el número de réplicas de un Deployment basándose en el uso de la CPU.

Aquí está la explicación de los parámetros:

- `kubectl autoscale deployment apache`: Este comando crea un HPA para el Deployment llamado "apache".
- `--cpu-percent=40`: Esto indica que el HPA debe ajustar el número de réplicas para mantener el uso de la CPU en el 40% de la capacidad solicitada.
- - `--memory-percent=50`: Esto indica que el HPA debe ajustar el número de réplicas para mantener el uso de la RAM en el 40% de la capacidad solicitada.
- `--min=1`: Este es el número mínimo de réplicas que el HPA mantendrá. Aquí está configurado en 1.
- `--max=8`: Este es el número máximo de réplicas que el HPA puede escalar. Aquí está configurado en 8.

Con este comando, Kubernetes ajustará dinámicamente el número de réplicas del Deployment "apache" según el uso de la CPU en el rango del 40% de la capacidad solicitada, con un mínimo de 1 réplica y un máximo de 8 réplicas.