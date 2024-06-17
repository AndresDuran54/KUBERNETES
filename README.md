# KUBERNETES

Claro, Kubernetes es una plataforma de orquestación de contenedores de código abierto diseñada para automatizar el despliegue, escalado y operación de aplicaciones en contenedores. Originalmente desarrollado por Google, Kubernetes ahora es mantenido por la Cloud Native Computing Foundation (CNCF).

### Componentes Principales de Kubernetes

Kubernetes se compone de varios componentes que se dividen en dos categorías principales: los componentes del plano de control (control plane) y los componentes del nodo.

#### 1. Componentes del Plano de Control

El plano de control gestiona y controla el clúster de Kubernetes, tomando decisiones sobre la administración del clúster y detectando y respondiendo a eventos en el clúster.

##### a. **kube-apiserver**

- **Descripción:** Es la implementación de la API de Kubernetes. Actúa como punto de entrada para todas las operaciones de administración del clúster.
- **Función:** Expone la API de Kubernetes y procesa las solicitudes REST, valida y configura datos para los objetos API (pods, servicios, etc.).

##### b. **etcd**

- **Descripción:** Es un almacén de datos clave-valor distribuido.
- **Función:** Almacena todos los datos de configuración del clúster, incluyendo el estado del clúster. Es crucial para la alta disponibilidad y persistencia de datos.

##### c. **kube-scheduler**

- **Descripción:** Se encarga de asignar pods a nodos específicos en el clúster.
- **Función:** Determina en qué nodo se ejecutará un pod en función de varios factores como la capacidad de recursos, restricciones y políticas de afinidad.

##### d. **kube-controller-manager**

- **Descripción:** Ejecuta los controladores de Kubernetes.
- **Función:** Cada controlador es un bucle de control que observa el estado compartido del clúster a través del kube-apiserver y realiza cambios intentando mover el estado actual hacia el estado deseado. Incluye controladores como el de replicación, control de nodos, y control de endpoints.

##### e. **cloud-controller-manager**

- **Descripción:** Gestiona la integración con los proveedores de servicios en la nube.
- **Función:** Permite que el clúster de Kubernetes interactúe con el proveedor de nube subyacente (provisionar y gestionar recursos como instancias de computación, balanceadores de carga, y almacenamiento).

#### 2. Componentes del Nodo

Los nodos son las máquinas en las que se ejecutan las aplicaciones en contenedores. Cada nodo contiene los servicios necesarios para ejecutar pods y está gestionado por los componentes del plano de control.

##### a. **kubelet**

- **Descripción:** Un agente que se ejecuta en cada nodo del clúster.
- **Función:** Se asegura de que los contenedores descritos en los objetos Pod se estén ejecutando y funcionando correctamente en el nodo.

##### b. **kube-proxy**

- **Descripción:** Un proxy de red que se ejecuta en cada nodo.
- **Función:** Mantiene las reglas de red en los nodos, permitiendo la comunicación entre los diferentes servicios y pods en el clúster.

##### c. **Container Runtime**

- **Descripción:** El software que se encarga de ejecutar los contenedores.
- **Función:** Kubernetes soporta varios runtime de contenedores, incluyendo Docker, containerd, y CRI-O.

### Otros Componentes Importantes

##### **Add-Ons**

Kubernetes también puede incluir varios complementos (add-ons) para extender sus funcionalidades:

- **DNS:** Un servicio DNS para el clúster, que permite a los pods y servicios descubrirse unos a otros.
- **Dashboard:** Una interfaz web para gestionar el clúster.
- **Metric Server:** Un servidor que recopila métricas del clúster y proporciona datos a la API de Kubernetes para el escalado automático.

### Arquitectura General de Kubernetes

![Arquitectura de Kubernetes](https://d33wubrfki0l68.cloudfront.net/d19571e95f354c3845eaf6a321d800f60bda44e7/f8390/docs/tutorials/kubernetes-basics/public/images/module_02_cluster.svg)

### Resumen

- **Kubernetes** es una plataforma para gestionar contenedores.
- **Plano de Control:** Gestiona el clúster (incluye kube-apiserver, etcd, kube-scheduler, kube-controller-manager, cloud-controller-manager).
- **Nodos:** Ejecutan los contenedores (incluyen kubelet, kube-proxy, y container runtime).

Kubernetes proporciona una solución robusta para gestionar aplicaciones contenedorizadas, permitiendo a los desarrolladores y operadores desplegar, escalar y mantener aplicaciones en un entorno altamente automatizado y resiliente.