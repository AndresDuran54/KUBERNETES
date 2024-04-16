# Persistent Volume

Un volumen persistente en Kubernetes es un tipo de recurso que proporciona almacenamiento de datos persistente para los contenedores en un clúster de Kubernetes. Estos volúmenes están diseñados para sobrevivir a la terminación de los pods y pueden ser montados en diferentes pods en caso de que se necesite acceso persistente a los datos.

Algunas características importantes de los volúmenes persistentes en Kubernetes incluyen:

1. **Persistencia de datos**: Los datos almacenados en un volumen persistente persisten incluso después de que se elimine el pod que los creó.

2. **Acceso compartido**: Los volúmenes persistentes pueden ser montados por múltiples pods al mismo tiempo, lo que permite el acceso compartido a los datos entre diferentes partes de una aplicación.

3. **Tipos de almacenamiento**: Kubernetes admite varios tipos de almacenamiento para volúmenes persistentes, incluidos almacenamientos en la nube, almacenamientos locales, almacenamientos en red y más.

4. **Administración flexible**: Los volúmenes persistentes pueden ser administrados de manera flexible a través de la definición de recursos en YAML, lo que permite a los administradores de clúster especificar cómo se deben configurar y administrar estos volúmenes.

En resumen, los volúmenes persistentes en Kubernetes son una forma de proporcionar almacenamiento persistente y accesible a los contenedores en un clúster de Kubernetes, lo que facilita el manejo de datos en aplicaciones distribuidas y escalables.

La etiqueta `persistentVolumeReclaimPolicy` en el archivo de configuración de un PersistentVolume (PV) especifica la política que se seguirá cuando el PersistentVolumeClaim (PVC) asociado a ese PV se elimine. Hay tres opciones comunes para esta etiqueta:

1. **Retain (Retener)**: Con esta política, el PV no se elimina automáticamente cuando el PVC asociado se elimina. En su lugar, el almacenamiento sigue estando disponible y se espera que el administrador de clústeres lo limpie manualmente si es necesario. Esto es útil si se necesita conservar los datos almacenados en el PV incluso después de que se elimine el PVC.

2. **Delete (Eliminar)**: Con esta política, el PV se elimina automáticamente cuando el PVC asociado se elimina. Esto significa que el almacenamiento también se libera, lo que puede ser útil si se desea que el almacenamiento se limpie junto con el PVC.

3. **Recycle (Reciclar)**: Esta política está en desuso y ya no se recomienda su uso. Anteriormente, esta política especificaba que el contenido del volumen se borraba cuando el PVC asociado se eliminaba. Sin embargo, esta política no maneja adecuadamente la limpieza de datos sensibles y, por lo tanto, se ha desaconsejado.

La elección de la política de reaprovechamiento de volumen persistente depende de los requisitos de la aplicación y de la estrategia de gestión de datos del clúster. Por ejemplo, si los datos son sensibles y deben conservarse incluso después de eliminar el PVC, se puede utilizar la política de retención. Si el almacenamiento debe liberarse para su reutilización después de eliminar el PVC, se puede utilizar la política de eliminación.

### Access Modes

En Kubernetes, los volúmenes persistentes pueden tener diferentes modos de acceso que determinan cómo pueden ser utilizados por los contenedores dentro de los pods. Los principales tipos de acceso para los volúmenes persistentes son los siguientes:

1. **ReadWriteOnce (RWO - Lectura y Escritura para Uno)**:
   - Este modo permite que un único nodo de Kubernetes monte el volumen y lo utilice tanto para lectura como para escritura.
   - Útil para aplicaciones que requieren un almacenamiento que solo puede ser accedido por un único pod a la vez.

2. **ReadOnlyMany (ROX - Solo Lectura para Muchos)**:
   - En este modo, múltiples nodos de Kubernetes pueden montar el volumen de forma simultánea, pero solo pueden leer datos de él. No se permite la escritura en el volumen desde varios nodos.
   - Ideal para aplicaciones que necesitan datos de solo lectura compartidos por varios pods.

3. **ReadWriteMany (RWX - Lectura y Escritura para Muchos)**:
   - Este modo permite que varios nodos de Kubernetes monten el volumen y lo utilicen tanto para lectura como para escritura de forma simultánea.
   - Útil para aplicaciones que necesitan acceder a un almacenamiento compartido en modo de lectura y escritura desde varios pods al mismo tiempo.

Estos modos de acceso proporcionan flexibilidad para satisfacer diferentes necesidades de almacenamiento en aplicaciones distribuidas ejecutadas en clústeres de Kubernetes. Es importante elegir el modo de acceso adecuado según los requisitos de la aplicación y la configuración del entorno.

# Persistent Volume Claim

En Kubernetes, un PersistentVolumeClaim (PVC) es un objeto que se utiliza para solicitar almacenamiento persistente de un PersistentVolume (PV). Un PVC permite a los usuarios especificar el tamaño, el modo de acceso y otros atributos del almacenamiento que necesitan para sus aplicaciones.

Cuando un usuario crea un PVC, Kubernetes encuentra un PersistentVolume disponible que coincida con los criterios especificados en el PVC, como el tamaño y el modo de acceso. Una vez que se encuentra un PV adecuado, Kubernetes lo asigna al PVC y lo vincula, lo que permite que los pods accedan al almacenamiento persistente mediante el PVC.

Los PVCs permiten que las aplicaciones definan sus necesidades de almacenamiento de una manera abstracta y portátil, lo que facilita la portabilidad de las aplicaciones entre diferentes entornos de Kubernetes. Además, los PVCs desacoplan la definición de almacenamiento de la implementación real, lo que permite a los administradores de clústeres gestionar de manera más eficiente los recursos de almacenamiento subyacentes.

