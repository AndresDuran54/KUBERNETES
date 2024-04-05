# ResourceQuota

Los `ResourceQuota` en Kubernetes son recursos que se utilizan para limitar la cantidad de recursos que pueden consumir los objetos dentro de un namespace específico. Proporcionan una forma de establecer cuotas en términos de CPU, memoria y otros recursos para los objetos dentro del namespace.

Algunos puntos clave sobre los `ResourceQuota`:

1. **Definición de límites**: Permiten definir límites en la cantidad de recursos que pueden ser consumidos por los objetos dentro del namespace. Esto ayuda a garantizar que los recursos del clúster se utilicen de manera eficiente y justa entre los diferentes equipos o aplicaciones que comparten el clúster.

2. **Recursos limitados**: Los `ResourceQuota` pueden limitar varios recursos, como CPU, memoria, número de pods, servicios, PVC (PersistentVolumeClaim), y otros recursos de Kubernetes.

3. **Administración de recursos**: Son útiles para la gestión de recursos en entornos compartidos o multi-tenancy, donde múltiples equipos o aplicaciones comparten el mismo clúster de Kubernetes. Permiten establecer políticas de asignación de recursos y garantizar que ningún equipo o aplicación monopolice los recursos del clúster.

4. **Notificación de cuotas**: Cuando se excede una cuota definida, Kubernetes puede generar eventos o notificaciones para informar a los administradores del clúster sobre el uso excesivo de recursos.

5. **Configuración por namespace**: Los `ResourceQuota` se aplican a nivel de namespace, lo que permite definir políticas de cuotas específicas para diferentes áreas, equipos o aplicaciones dentro del clúster.

En resumen, los `ResourceQuota` son una herramienta importante para la gestión y el control de recursos en entornos de Kubernetes, permitiendo establecer límites y políticas de asignación de recursos para garantizar un uso eficiente y equitativo del clúster.