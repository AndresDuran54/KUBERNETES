# Limit Range
Los `LimitRange` en Kubernetes sirven para establecer límites predeterminados y restricciones en los recursos de los contenedores dentro de un clúster. Estas restricciones incluyen límites en la cantidad de CPU y memoria que pueden usar los contenedores, así como valores predeterminados para las solicitudes de recursos.

Aquí hay algunas razones importantes por las que se utilizan los `LimitRange`:

1. **Gestión de recursos**: Los `LimitRange` ayudan a administrar y controlar el uso de recursos en un clúster de Kubernetes al establecer límites máximos y mínimos para la CPU y la memoria que pueden consumir los contenedores. Esto evita que un contenedor consuma todos los recursos disponibles y afecte negativamente a otros contenedores en el mismo nodo.

2. **Establecer estándares de recursos**: Los `LimitRange` permiten establecer estándares de recursos para todos los contenedores en un espacio de nombres (namespace). Esto garantiza que todos los contenedores cumplan con ciertos requisitos mínimos de recursos, lo que puede ser importante para garantizar un rendimiento predecible y evitar problemas de agotamiento de recursos.

3. **Prevención de abuso de recursos**: Al establecer límites máximos en los recursos que un contenedor puede usar, los `LimitRange` ayudan a prevenir el abuso de recursos y a garantizar una distribución equitativa de recursos en el clúster.

En resumen, los `LimitRange` son una herramienta importante para establecer políticas de gestión de recursos y garantizar un uso eficiente y equitativo de los recursos en un clúster de Kubernetes.

# Tag maxLimitRequestRatio 
`maxLimitRequestRatio` es un parámetro que se puede configurar dentro de un objeto `LimitRange` en Kubernetes. Este parámetro se utiliza para especificar una relación máxima permitida entre los recursos de límite (`limits`) y los recursos de solicitud (`requests`) para los contenedores en un namespace.

En un `LimitRange`, `maxLimitRequestRatio` se define como una proporción entre los recursos límite y los recursos de solicitud. Por ejemplo, si `maxLimitRequestRatio` se establece en 2, significa que los recursos límite (`limits`) pueden ser hasta dos veces mayores que los recursos de solicitud (`requests`). Si un contenedor excede esta relación máxima, se considera que viola la política de limitación del namespace.

Este parámetro es útil para establecer límites razonables en los recursos que pueden solicitar los contenedores dentro de un namespace, lo que ayuda a evitar un uso excesivo de recursos y a garantizar una distribución equitativa de los recursos entre los distintos contenedores.