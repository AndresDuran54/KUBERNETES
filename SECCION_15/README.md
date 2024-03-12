# Instalar kudeadm

`kubeadm` es una herramienta de línea de comandos que facilita la inicialización y configuración de clústeres de Kubernetes. Es parte del proyecto Kubernetes y está diseñada para automatizar muchas de las tareas asociadas con la creación y gestión de un clúster de Kubernetes.

Las principales funciones de `kubeadm` incluyen:

1. **Inicialización de clúster**: `kubeadm` puede inicializar un clúster de Kubernetes, configurando los componentes principales como el controlador (master) y los nodos de trabajo (worker). Esto simplifica significativamente el proceso de configuración inicial del clúster.

2. **Admisión de nuevos nodos**: `kubeadm` facilita la adición de nuevos nodos al clúster, automatizando muchas de las tareas involucradas en la configuración de un nuevo nodo de trabajo.

3. **Configuración segura**: `kubeadm` aplica las mejores prácticas de seguridad al configurar el clúster, como la generación de certificados TLS y la configuración de políticas de acceso adecuadas.

4. **Integración con herramientas existentes**: `kubeadm` está diseñado para integrarse bien con otras herramientas y flujos de trabajo, lo que facilita su incorporación en entornos existentes.

En resumen, `kubeadm` es una herramienta fundamental para administrar clústeres de Kubernetes, especialmente en entornos donde se requiere una configuración y administración automatizada y repetible.

### 1. Set SELinux in permissive mode (effectively disabling it):

SELinux (Security-Enhanced Linux) es un conjunto de extensiones del núcleo del sistema operativo Linux que proporciona un control de acceso obligatorio (MAC) al sistema. Fue desarrollado originalmente por la NSA (Agencia de Seguridad Nacional) de los Estados Unidos y se integró en el núcleo de Linux en la versión 2.6.

El propósito principal de SELinux es aumentar la seguridad del sistema operativo Linux imponiendo restricciones adicionales sobre qué acciones pueden realizar los usuarios y los programas en el sistema. Esto se logra mediante la aplicación de políticas de seguridad predefinidas que especifican qué recursos pueden acceder los procesos y qué operaciones pueden realizar en esos recursos.

A diferencia del modelo de control de acceso discrecional (DAC) tradicional de Linux, en el que los permisos de acceso son definidos por el propietario de los recursos, SELinux implementa un modelo de control de acceso obligatorio (MAC) en el que los permisos son definidos por políticas de seguridad y son aplicados de manera obligatoria, independientemente de los permisos definidos por el propietario del recurso.

Esto significa que SELinux puede prevenir y mitigar una amplia gama de ataques de seguridad, como la escalada de privilegios, la ejecución de código malicioso y el acceso no autorizado a recursos del sistema.

Sin embargo, debido a su naturaleza altamente restrictiva, SELinux puede requerir una configuración y administración cuidadosas para evitar conflictos con aplicaciones y servicios legítimos. En algunos casos, puede ser necesario ajustar las políticas de SELinux para permitir ciertas operaciones o deshabilitar SELinux temporalmente para resolver problemas de compatibilidad.

```bash
# Set SELinux in permissive mode (effectively disabling it)
sudo setenforce 0
sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config
```

Estos comandos son utilizados típicamente en sistemas basados en Linux, como CentOS, Fedora, o RHEL, donde SELinux (Security-Enhanced Linux) está habilitado de forma predeterminada para proporcionar un control de acceso obligatorio (MAC) al sistema.

Aquí está lo que hacen estos comandos:

1. `sudo setenforce 0`: Este comando establece SELinux en modo permisivo. En este modo, SELinux todavía registrará las violaciones de política que encuentra, pero no las aplicará, lo que permite que las operaciones que de otro modo serían bloqueadas se completen sin restricciones.

2. `sudo sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/' /etc/selinux/config`: Este comando modifica el archivo de configuración de SELinux (`/etc/selinux/config`) para que la configuración persista después de reiniciar el sistema. Reemplaza la línea `SELINUX=enforcing` por `SELINUX=permissive`, lo que configura SELinux para que se inicie en modo permisivo automáticamente en el próximo arranque del sistema.

Es importante entender que cambiar SELinux a modo permisivo o deshabilitarlo por completo puede tener implicaciones importantes para la seguridad del sistema. Si bien puede ser útil temporalmente para solucionar problemas de compatibilidad con aplicaciones, se recomienda encarecidamente investigar y abordar las políticas de SELinux específicas para su aplicación en lugar de simplemente deshabilitar o poner en modo permisivo SELinux.

El comando que proporcionaste utilizando `sed -i 's/^SELINUX=enforcing$/SELINUX=permissive/'` es una expresión de `sed` que se utiliza para editar el contenido de un archivo de texto de forma in situ.

Aquí está la explicación detallada de cada parte del comando:

- `sed`: El comando utilizado para manipular texto en Linux.
- `-i`: Una opción de `sed` que significa "in situ" o "edición en línea", lo que indica que los cambios se deben hacer directamente en el archivo original.
- `'s/^SELINUX=enforcing$/SELINUX=permissive/'`: Esta es la expresión de sustitución que se pasará a `sed` para editar el archivo. Tiene el formato `'s/patrón_a_buscar/patrón_de_reemplazo/'`, donde:
  - `s`: Indica que se realizará una sustitución.
  - `^SELINUX=enforcing$`: Es el patrón a buscar. En este caso, `^` representa el inicio de la línea, `$` representa el final de la línea, y `SELINUX=enforcing` es la cadena completa que se buscará.
  - `SELINUX=permissive`: Es el patrón de reemplazo. Cuando se encuentre una línea que coincida exactamente con `SELINUX=enforcing`, se reemplazará con `SELINUX=permissive`.

En resumen, este comando busca en un archivo de texto la línea que comienza exactamente con `SELINUX=enforcing` y la reemplaza por `SELINUX=permissive`. Esto es útil, por ejemplo, para cambiar la configuración de SELinux de "enforcing" a "permissive" directamente en el archivo de configuración sin necesidad de editarlo manualmente.

Este comando `sudo yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes` se utiliza en sistemas Linux basados en RPM (como CentOS, Red Hat Enterprise Linux, o Fedora) para instalar los paquetes `kubelet`, `kubeadm`, y `kubectl` utilizando el gestor de paquetes `yum`.

Aquí está la explicación detallada de cada parte del comando:

- `sudo`: Ejecuta el comando con privilegios de superusuario, lo que puede ser necesario para instalar paquetes en el sistema.
- `yum`: Es el gestor de paquetes utilizado en sistemas Linux basados en RPM para instalar, actualizar y administrar paquetes de software.
- `install`: Indica que se desea instalar los paquetes especificados.
- `-y`: Asume "sí" como respuesta a todas las preguntas, lo que significa que el comando no solicitará confirmación antes de instalar los paquetes.
- `kubelet kubeadm kubectl`: Son los nombres de los paquetes que se desean instalar. Estos son componentes del software de Kubernetes.
- `--disableexcludes=kubernetes`: Esta opción se utiliza para deshabilitar cualquier exclusión de paquetes definida para el repositorio de `kubernetes`. Por lo tanto, se instalarán todos los paquetes relevantes, incluso si están excluidos por defecto.

En resumen, este comando instalará los paquetes `kubelet`, `kubeadm`, y `kubectl` en el sistema utilizando `yum`, asegurándose de que se instalen incluso si están excluidos por defecto en el repositorio `kubernetes`.

El comando `sudo systemctl enable --now kubelet` se utiliza en sistemas Linux que utilizan el sistema de inicio de systemd (como CentOS, Fedora, y otras distribuciones modernas) para habilitar y activar el servicio `kubelet`. Este servicio es esencial en un clúster de Kubernetes, ya que es responsable de administrar los nodos del clúster y asegurarse de que estén en un estado saludable.

Aquí está la explicación detallada de cada parte del comando:

- `sudo`: Ejecuta el comando con privilegios de superusuario, lo que puede ser necesario para realizar cambios en la configuración del sistema.
- `systemctl`: Es la utilidad de systemd utilizada para controlar los servicios del sistema, como iniciar, detener, habilitar y deshabilitar.
- `enable`: Esta opción indica que se desea habilitar el servicio `kubelet` para que se inicie automáticamente en el arranque del sistema.
- `--now`: Esta opción indica que se desea iniciar el servicio `kubelet` inmediatamente después de habilitarlo. Sin esta opción, el servicio se habilitaría pero no se iniciaría hasta que se reinicie el sistema o se inicie manualmente.
- `kubelet`: Es el nombre del servicio que se desea habilitar y activar. Este es el servicio principal responsable de ejecutar y supervisar los contenedores en un nodo de Kubernetes.

En resumen, este comando habilitará y activará el servicio `kubelet`, lo que garantizará que se inicie automáticamente en el arranque del sistema y se inicie de inmediato. Esto es fundamental para garantizar el funcionamiento adecuado de un clúster de Kubernetes.