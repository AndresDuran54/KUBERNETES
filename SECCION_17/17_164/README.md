# Kubernetes

Kubernetes Metrics Server es un componente de Kubernetes diseñado para recopilar métricas de recursos y uso de CPU y memoria de los nodos y los contenedores en un clúster de Kubernetes. Proporciona datos sobre el rendimiento de los recursos del clúster, lo que permite a los administradores y desarrolladores monitorear y escalar sus aplicaciones de manera más eficiente.

Algunas de las características clave del Metrics Server incluyen:

1. **Recopilación de métricas en tiempo real:** El Metrics Server recopila y almacena métricas de uso de recursos en tiempo real, lo que proporciona una visión actualizada del estado del clúster.

2. **Integración con herramientas de monitoreo:** Las métricas recopiladas por el Metrics Server se pueden integrar con herramientas de monitoreo externas, como Prometheus, Grafana, o herramientas de autoscaling de Kubernetes.

3. **Escalabilidad:** El Metrics Server está diseñado para ser escalable y eficiente, lo que permite su implementación en clústeres de cualquier tamaño.

En resumen, Kubernetes Metrics Server es una parte integral de la infraestructura de monitoreo de Kubernetes, permitiendo a los usuarios supervisar el rendimiento y la utilización de recursos de sus aplicaciones y clústeres.

## Instalar Metric Server en un Cluster Real

#### 1. Aplicar la configuración en nuestro Cluster
El comando que has proporcionado utiliza `kubectl` para aplicar la configuración del Metrics Server en un clúster de Kubernetes. Esta configuración se obtiene desde un archivo YAML alojado en GitHub, que contiene la información necesaria para desplegar el Metrics Server en el clúster.

Aquí está el desglose del comando:

- `kubectl apply`: Este comando se utiliza para aplicar la configuración especificada en un archivo YAML o JSON al clúster de Kubernetes.
- `-f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml`: Esta parte del comando especifica la ubicación del archivo YAML que contiene la configuración del Metrics Server. En este caso, el archivo se encuentra en GitHub, y el enlace proporcionado es la URL directa al archivo YAML.

Al ejecutar este comando, `kubectl` descargará el archivo YAML del Metrics Server desde GitHub y aplicará la configuración en tu clúster de Kubernetes. Esto incluirá la creación de los recursos necesarios, como los Deployment, ServiceAccount, Role, RoleBinding, y otros, que son necesarios para desplegar y ejecutar el Metrics Server en tu clúster.