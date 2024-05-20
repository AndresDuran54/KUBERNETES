# Roles

En Kubernetes, un "rol" (Role) es un objeto que define un conjunto de permisos o autorizaciones específicas para acceder y realizar operaciones en recursos dentro de un clúster. Los roles son parte del sistema de Control de Acceso Basado en Roles (RBAC), que permite administrar de manera granular quién puede hacer qué dentro de un clúster de Kubernetes.

Un rol consiste en una lista de reglas (rules) que especifican qué acciones están permitidas en qué recursos dentro de un API Group particular. Por ejemplo, un rol podría permitir a un usuario crear, leer, actualizar o eliminar pods en el API Group "core".

Cuando se crea un rol, se asocia con un namespace específico o con todo el clúster (en cuyo caso se llama un "ClusterRole"). Esto determina el alcance del rol y dónde se aplicarán sus permisos.

Para utilizar un rol, se debe vincular con uno o más usuarios, grupos de usuarios o servicios de Kubernetes mediante un objeto llamado "RoleBinding" o "ClusterRoleBinding". Esto establece la relación entre el rol y los sujetos a los que se les aplicarán sus permisos.

En resumen, un rol en Kubernetes es una herramienta crucial para controlar quién puede hacer qué dentro de un clúster, proporcionando una capa de seguridad y control de acceso muy necesaria en entornos de producción.

## Api Group

En Kubernetes, un API Group es una forma de agrupar recursos relacionados bajo una única interfaz. Los recursos en Kubernetes se exponen a través de una API RESTful, y cada recurso está asociado con un conjunto de operaciones CRUD (crear, leer, actualizar, eliminar). Los recursos pueden ser cosas como pods, servicios, volúmenes, etc.

Los API Groups proporcionan una forma de organizar estos recursos de manera lógica y coherente. Por ejemplo, el API Group "core" contiene los recursos básicos como pods, servicios y namespaces. Otros API Groups pueden contener recursos específicos de ciertas características o extensiones, como el API Group "apps" que contiene recursos relacionados con las aplicaciones como deployments y statefulsets.

Los roles en Kubernetes, como los roles de RBAC (Control de Acceso Basado en Roles), permiten definir permisos granulares para usuarios y servicios dentro de un clúster de Kubernetes. Al definir roles, puedes especificar qué acciones pueden realizar en los recursos de un determinado API Group. Por lo tanto, el API Group se convierte en una unidad lógica para gestionar los permisos de acceso a recursos específicos dentro de Kubernetes.

En Kubernetes, hay varios API Groups que organizan los recursos de acuerdo con su funcionalidad. Algunos de los API Groups más comunes son:

1. **core**: Este es el API Group principal que contiene los recursos básicos de Kubernetes, como pods, servicios, namespaces, eventos, secretos, etc.

2. **apps**: Contiene recursos relacionados con las aplicaciones, como deployments, replicasets, daemonsets, statefulsets, etc.

3. **batch**: Aquí se encuentran los recursos relacionados con trabajos y tareas por lotes, como jobs y cronjobs.

4. **extensions**: Este API Group solía ser utilizado para características de Kubernetes que estaban en versión beta, pero muchos de sus recursos han sido graduados a API Groups específicos. A partir de Kubernetes 1.16, ya no se recomienda su uso.

5. **networking.k8s.io**: Contiene recursos relacionados con la configuración de la red en Kubernetes, como servicios de red, políticas de red, etc.

6. **storage.k8s.io**: Aquí se encuentran los recursos relacionados con el almacenamiento, como almacenamientos persistentes, volúmenes persistentes, etc.

7. **autoscaling**: Contiene recursos relacionados con el escalado automático, como horizontalpodautoscalers.

8. **authentication.k8s.io** y **authorization.k8s.io**: Contienen recursos relacionados con la autenticación y autorización en Kubernetes, como tokens de servicio, roles, rolebindings, etc.

Estos son solo algunos ejemplos de API Groups comunes en Kubernetes. Dependiendo de las extensiones y características adicionales que estén habilitadas en tu clúster de Kubernetes, es posible que encuentres otros API Groups específicos.

## Verbs

En Kubernetes, los verbos que se utilizan para definir acciones sobre los recursos son los siguientes:

1. **create**: Permite crear un recurso.
2. **get**: Permite obtener información sobre un recurso existente.
3. **list**: Permite obtener una lista de recursos.
4. **update**: Permite modificar un recurso existente.
5. **delete**: Permite eliminar un recurso existente.
6. **watch**: Permite observar cambios en un recurso en tiempo real.
7. **patch**: Permite realizar modificaciones específicas en un recurso sin reemplazarlo por completo.
8. **proxy**: Permite acceder a un recurso a través de un proxy.
9. **redirect**: Permite redirigir el tráfico a un recurso.
10. **connect**: Permite establecer una conexión a un recurso.
11. **attach**: Permite adjuntar un recurso a otro.
12. **exec**: Permite ejecutar un comando dentro de un contenedor en un pod.
13. **port-forward**: Permite reenviar puertos de un recurso.
14. **bind**: Permite vincular un recurso.
15. **escalate**: Permite obtener privilegios adicionales.

Estos verbos se utilizan en combinación con los recursos y los API Groups para definir reglas de acceso en los roles y los ClusterRoles en Kubernetes.