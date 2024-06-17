# Bootstraping 

Bootstrapping es el proceso de crear un nuevo clúster de Kubernetes desde cero y ponerlo en funcionamiento. Arrancar un clúster de Kubernetes implica configurar el plano de control y los nodos trabajadores y determinar qué nodo tiene la información correcta con la que todos los demás nodos deben sincronizarse.

- Crear el cluster y nodo maestro (Plano de control)
  -
    Primero debemos de elegir el plugin Network, ya que la configuración del cluster dependerá
    de este. Un plugin de red (network plugin) en Kubernetes es un componente esencial que se utiliza para proporcionar conectividad de red entre los pods y aplicar políticas de red dentro de un clúster. Estos plugins gestionan la configuración de red y permiten que los contenedores se comuniquen entre sí y con recursos externos.

    Los plugins de red en Kubernetes son responsables de varias tareas, entre las que se incluyen:

    1. **Asignación de direcciones IP**: Los plugins de red asignan direcciones IP a los pods para que puedan comunicarse entre sí y con el mundo exterior.

    2. **Enrutamiento**: Facilitan la comunicación de red entre los pods dentro del clúster, asegurando que los paquetes de datos se enruten correctamente.

    3. **Seguridad de red**: Los plugins de red permiten la aplicación de políticas de seguridad de red, como control de acceso basado en reglas, a fin de restringir el tráfico de red entre pods y proteger la infraestructura del clúster.

    4. **Aislamiento de red**: Proporcionan aislamiento de red entre los pods para evitar interferencias y garantizar la privacidad y seguridad de las comunicaciones.

    5. **Integración con otros servicios**: Algunos plugins de red pueden integrarse con servicios externos, como firewalls y servicios de descubrimiento de servicios, para proporcionar funcionalidades adicionales de red y seguridad.

    Hay varios plugins de red disponibles para Kubernetes, cada uno con sus propias características y funcionalidades. Algunos ejemplos comunes de plugins de red incluyen Calico, Flannel, Weave, Cilium, entre otros. La elección del plugin de red adecuado depende de los requisitos específicos del entorno y las preferencias del usuario.

    ### Calico
    Calico es uno de los plugins de red más populares y ampliamente utilizados en el ecosistema de Kubernetes. Es una solución de red y seguridad de código abierto diseñada para proporcionar conectividad de red segura y escalable para entornos de contenedores, especialmente en clústeres Kubernetes. Aquí hay algunas características y aspectos importantes de Calico:

    6. **Enrutamiento basado en IP**: Calico utiliza enrutamiento basado en IP para conectar workloads en un clúster Kubernetes, lo que permite una conectividad de red eficiente y escalable.

    7. **Políticas de seguridad**: Calico permite definir políticas de seguridad de red a nivel de aplicación para restringir el tráfico entre workloads según reglas específicas, como puertos y direcciones IP. Esto proporciona un control granular sobre las comunicaciones de red dentro del clúster.

    8. **Escalabilidad y rendimiento**: Calico está diseñado para ser altamente escalable y eficiente en entornos de gran escala. Su arquitectura distribuida y liviana asegura un rendimiento óptimo incluso en clústeres Kubernetes grandes y complejos.

    9. **Integración con Kubernetes**: Calico se integra estrechamente con Kubernetes y se despliega como un complemento para proporcionar funcionalidades avanzadas de red y seguridad dentro del clúster.

    10. **Soporte de políticas de red avanzadas**: Calico admite políticas de red avanzadas, como la segmentación de red, el aislamiento de recursos y la integración con proveedores de identidad y acceso, lo que lo hace adecuado para una amplia gama de casos de uso y entornos empresariales.

    En resumen, Calico es una solución robusta y flexible para la red y la seguridad en entornos de Kubernetes, que ofrece un rendimiento excepcional, capacidades avanzadas de seguridad y una integración perfecta con el ecosistema de Kubernetes.

    ## 1. Desahabilitar las áreas de intercambio de mi sistema

    #### 1.1 Comando para listar todas las áreas de intercambio del sistema listadas en /proc/swaps
    ```sh
    swapon -s
    ```

    #### 1.2 Comando para deshabilitar todas las áreas de intercambio listadas en /proc/swaps
    ```sh
    sudo swapoff -a
    ```

    #### 1.3 Deshabilitamos del sistema las áreas de intercambio, para que no se vuelvan a arrancar al iniciar el servidor

    Para eso vamos al 
    ```sh
      # /etc/fstab: static file system information.
      #
      # Use 'blkid' to print the universally unique identifier for a
      # device; this may be used with UUID= as a more robust way to name devices
      # that works even if disks are added and removed. See fstab(5).
      #
      # <file system> <mount point>   <type>  <options>       <dump>  <pass>
      # / was on /dev/nvme0n1p5 during installation
      UUID=f1dd64ac-57de-44c6-9095-d69007e1567b /               ext4    errors=remount-ro 0       1
      # /boot/efi was on /dev/nvme0n1p1 during installation
      UUID=6CA4-28DB  /boot/efi       vfat    umask=0077      0       1

      # COMENTAMOS ESTA LINEA QUE INDICA QUE SE DEBE DE MONTAR ESTE AREA DE INTERCAMBIO AL ARRANCAR
      # /swapfile                                 none            swap    sw              0       0
    ```

    ## 2. Instalamos Kubectl, kubeadm y kubelet

    #### 2.1 Actualice el índice del paquete apt e instale los paquetes necesarios para usar el repositorio apt de Kubernetes:

    ```sh
    sudo apt-get update
    # apt-transport-https may be a dummy package; if so, you can skip that package
    sudo apt-get install -y apt-transport-https ca-certificates curl gpg
    ```

    #### 2.2 Descargue la clave de firma pública para los repositorios de paquetes de Kubernetes. Se utiliza la misma clave de firma para todos los repositorios, por lo que puede ignorar la versión en la URL:

    ```sh
    # If the directory `/etc/apt/keyrings` does not exist, it should be created before the curl command, read  the note below.
    # sudo mkdir -p -m 755 /etc/apt/keyrings  
    curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.30/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg
    ```

    #### 2.3 Agregue el repositorio apto de Kubernetes apropiado. Tenga en cuenta que este repositorio tiene paquetes solo para Kubernetes 1.30; para otras versiones menores de Kubernetes, debe cambiar la versión menor de Kubernetes en la URL para que coincida con la versión menor deseada (también debe verificar que esté leyendo la documentación de la versión de Kubernetes que planea instalar).

    ```sh
    # This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
    echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.30/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list
    ```

    #### 2.4 Actualice el índice del paquete apt, instale kubelet, kubeadm y kubectl y fije su versión:

    ```sh
    sudo apt-get update
    sudo apt-get install -y kubelet kubeadm kubectl
    sudo apt-mark hold kubelet kubeadm kubectl
    ```

    #### 2.5 (Opcional) Habilite el servicio kubelet antes de ejecutar kubeadm:

    ```sh
    sudo systemctl enable --now kubelet
    ```

    ### 1. Iniciamos un clúster de Kubernetes en un nodo maestro (Plano de control)

    #### 1.1 Comando para levantar el cluster con el nodo maestro.
    
    ```sh
    sudo kubeadm init --pod-network-cidr=192.168.0.0/16
    ```

    El comando `sudo kubeadm init --pod-network-cidr=192.168.0.0/16` se utiliza para inicializar un clúster de Kubernetes en un nodo maestro. Aquí está la explicación de cada parte del comando:

    - `sudo`: Es un comando utilizado en sistemas basados en Unix/Linux que permite a los usuarios ejecutar comandos con privilegios de superusuario (root).

    - `kubeadm init`: Es un comando de Kubernetes utilizado para inicializar un clúster de Kubernetes. Este comando configura el nodo actual como el nodo maestro del clúster.

    - `--pod-network-cidr=192.168.0.0/16`: Es una bandera que se utiliza para especificar el rango de direcciones IP que se asignará a los pods en el clúster. En este caso, se establece el rango de direcciones IP para los pods como `192.168.0.0/16`. Este parámetro es importante para la configuración de la red en el clúster.

    Una vez que se ejecuta este comando, kubeadm realizará una serie de tareas para inicializar el clúster, incluyendo la configuración del nodo maestro, la inicialización del plano de control de Kubernetes, y la generación de los archivos de configuración necesarios para unirse a los nodos del clúster. También proporcionará instrucciones adicionales para configurar el entorno y unir los nodos al clúster.

    #### 1.2 Creamos la carpeta .kube en nuestro HOME

    ```sh
    mkdir -p $HOME/.kube
    ```
    
    Este comando crea el directorio .kube en su directorio de inicio si aún no existe. Este directorio es donde kubectl busca su archivo de configuración.

    #### 1.3. Copiamos el archivo de configuración

    ```sh
    sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
    ```

    Este comando copia el archivo de configuración del clúster de Kubernetes de /etc/kubernetes/admin.conf a $HOME/.kube/config. Este archivo de configuración contiene la información necesaria para que kubectl se comunique con el clúster de Kubernetes.

    #### 1.4. Nos otorgamos permisos de acceso al archivo y nos declaramos dueños del archivo

    ```sh
    sudo chown $(id -u):$(id -g) $HOME/.kube/config
    ```

    Este comando cambia el propietario y el grupo del archivo `$HOME/.kube/config` al propietario y grupo del usuario que está ejecutando el comando actualmente. Aquí está el desglose:

    - `sudo`: Ejecuta el comando con privilegios de superusuario para asegurarse de que tiene los permisos necesarios para cambiar el propietario del archivo.

    - `chown`: Es el comando utilizado en sistemas Unix y Linux para cambiar el propietario y el grupo de un archivo o directorio.

    - `$(id -u)`: Esto se sustituye por el ID de usuario (UID) del usuario actual. `id -u` es un comando que devuelve el ID de usuario del usuario actual.

    - `$(id -g)`: Esto se sustituye por el ID de grupo (GID) del usuario actual. `id -g` es un comando que devuelve el ID de grupo principal del usuario actual.

    - `$HOME/.kube/config`: Es la ruta al archivo de configuración de kubectl que se ha copiado previamente. `$HOME` es una variable de entorno que apunta al directorio de inicio del usuario actual.

    En resumen, este comando establece el propietario y el grupo del archivo de configuración de kubectl en el mismo propietario y grupo que el usuario actual que ejecuta el comando. Esto asegura que el usuario tenga los permisos necesarios para acceder y modificar el archivo de configuración.

    ### 2. Instalamos Calico

    #### 2.1. Instale el operador Tigera Calico y las definiciones de recursos personalizadas.

    ```sh
    kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.27.2/manifests/tigera-operator.yaml
    ```

    El comando `kubectl create -f` se utiliza para crear recursos de Kubernetes utilizando un archivo de manifiesto YAML o JSON. En este caso, estás utilizando un archivo YAML alojado en un repositorio en línea.

    Aquí está el desglose del comando:

    - `kubectl create`: Este es el comando principal de Kubernetes para crear recursos.
      
    - `-f`: Especifica que estás proporcionando un archivo de manifiesto YAML o JSON para crear recursos.

    - `https://raw.githubusercontent.com/projectcalico/calico/v3.27.2/manifests/tigera-operator.yaml`: Es la URL del archivo YAML que contiene la definición del recurso que deseas crear. En este caso, estás creando el operador de Tigera para Calico.

    Al ejecutar este comando, Kubernetes descargará el archivo de manifiesto del URL proporcionado y creará los recursos especificados en tu clúster. Esto puede incluir despliegos, servicios, roles, etc., según lo definido en el archivo YAML.

    #### 2.2. Configurar el archivo /etc/containerd/config.toml

    ```toml
    version = 2
    [plugins]
      [plugins."io.containerd.grpc.v1.cri"]
      [plugins."io.containerd.grpc.v1.cri".containerd]
          [plugins."io.containerd.grpc.v1.cri".containerd.runtimes]
            [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc]
              runtime_type = "io.containerd.runc.v2"
              [plugins."io.containerd.grpc.v1.cri".containerd.runtimes.runc.options]
                SystemdCgroup = true
    ```

    #### 2.3. Quitar el tain de node control-plane

    El comando `kubectl taint` en Kubernetes se utiliza para modificar la tolerancia de un nodo a ciertas condiciones. Un taint es una etiqueta adjunta a un nodo que indica ciertas restricciones o condiciones especiales para programar pods en ese nodo. 

    En este caso específico, el comando:

    ```bash
    kubectl taint nodes --all node-role.kubernetes.io/control-plane-
    ```

    Está eliminando el taint `node-role.kubernetes.io/control-plane-` de todos los nodos en el clúster. Este taint es comúnmente utilizado para marcar nodos que forman parte del plano de control de Kubernetes, lo que significa que son nodos maestros o controladores del clúster.

    Eliminar este taint permite que los pods que no toleran este taint puedan ser programados en estos nodos. En algunos casos, esto puede ser útil si necesitas desplegar pods de aplicaciones regulares en nodos que normalmente se reservarían para componentes del plano de control.

    Sin embargo, debes tener cuidado al quitar taints de nodos, ya que podría afectar el comportamiento y la confiabilidad del clúster si se programan pods que no están diseñados para ejecutarse en nodos de control. Es importante comprender el impacto de esta acción en tu entorno antes de ejecutarla.

    #### 2.4. Obtener un token para unir nodos worker al cluster


    El comando `kubeadm token create --print-join-command` en Kubernetes se utiliza para generar un nuevo token de unión y mostrar el comando de unión que los nodos worker deben ejecutar para unirse al clúster.

    Al ejecutar este comando, se generará un nuevo token de unión y se mostrará el comando que debe ejecutar un nodo worker para unirse al clúster. Este comando suele incluir el token generado, así como la dirección y el puerto del servidor de control al que el nodo worker debe conectarse para unirse al clúster.

    Por ejemplo, el resultado podría verse así:

    ```bash
    kubeadm join 10.0.0.22:6443 --token abcdef.1234567890abcdef \
        --discovery-token-ca-cert-hash sha256:1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef
    ```

    El nodo worker puede ejecutar este comando para unirse al clúster, proporcionando así la información necesaria para autenticarse y **establecer** la conexión con el servidor de control.

    En caso falle, podemos probar con lo siguiente:

    ```sh
    sudo rm /etc/containerd/config.toml
    sudo systemctl restart containerd
    ```

    Eliminar el archivo de configuración de containerd (`/etc/containerd/config.toml`) y luego reiniciar el servicio de containerd (`sudo systemctl restart containerd`) podría haber resuelto el problema si había algún problema con la configuración anterior de containerd.

    Al eliminar el archivo de configuración, containerd volverá a utilizar la configuración predeterminada, lo que podría solucionar cualquier conflicto o problema que estuviera causando la comunicación fallida entre el kubelet y containerd.

    Es posible que el archivo de configuración (`config.toml`) haya sido modificado incorrectamente o que contenga configuraciones incorrectas que estén interfiriendo con el funcionamiento adecuado de containerd. Al eliminar este archivo y reiniciar el servicio, containerd vuelve a su estado predeterminado y puede resolver el problema.

    Es importante recordar que eliminar archivos de configuración puede tener implicaciones en el funcionamiento de un servicio, y siempre es recomendable hacer una copia de seguridad o revisar la configuración antes de eliminarla. Sin embargo, en este caso, parece haber resuelto el problema que estabas experimentando con el kubelet y containerd.