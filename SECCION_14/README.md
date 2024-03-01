# Kubeconfig

**kubeconfig** es un archivo de configuración utilizado por la herramienta de línea de comandos `kubectl` en Kubernetes. Este archivo almacena información sobre clústeres, usuarios y contextos, permitiendo a `kubectl` interactuar con clústeres de Kubernetes de manera sencilla y configurada.

### Ubicación en Linux:

El archivo kubeconfig suele encontrarse en la ruta `~/.kube/config`. Si no existe, `kubectl` utiliza configuraciones predeterminadas.

### Estructura básica:

El kubeconfig es un archivo YAML con varias secciones. A continuación, se presenta una estructura básica:

```yaml
apiVersion: v1
kind: Config
clusters:
- name: nombre-del-cluster
  cluster:
    server: URL-del-cluster
    certificate-authority: ruta/al/authority.pem
contexts:
- name: nombre-del-contexto
  context:
    cluster: nombre-del-cluster
    user: nombre-del-usuario
current-context: nombre-del-contexto-actual
users:
- name: nombre-del-usuario
  user:
    client-certificate: ruta/al/certificado.pem
    client-key: ruta/al/llave-privada.pem
```
## Componentes clave
**Clusters:**
- **Definición:** Un clúster en el kubeconfig de Kubernetes es una especificación del entorno de un clúster, incluyendo la información necesaria para autenticarse y comunicarse con el servidor del clúster.
- **Estructura:**
  ```yaml
  clusters:
  - name: nombre-del-cluster
    cluster:
      server: URL-del-cluster
      certificate-authority: ruta/al/authority.pem
  ```
- **Explicación:**
  - **name:** Nombre descriptivo del clúster.
  - **cluster:**
    - **server:** URL del servidor del clúster.
    - **certificate-authority:** Ruta al archivo de certificado de autoridad (CA) para validar el servidor.

**Contexts:**
- **Definición:** Un contexto en el kubeconfig de Kubernetes combina un clúster y un usuario en una configuración única que define el entorno en el que se ejecutarán los comandos de `kubectl`.
- **Estructura:**
  ```yaml
  contexts:
  - name: nombre-del-contexto
    context:
      cluster: nombre-del-cluster
      user: nombre-del-usuario
  ```
- **Explicación:**
  - **name:** Nombre descriptivo del contexto.
  - **context:**
    - **cluster:** Nombre del clúster asociado al contexto.
    - **user:** Nombre del usuario asociado al contexto.

**Users:**
- **Definición:** Un usuario en el kubeconfig de Kubernetes especifica cómo `kubectl` autenticará al usuario con el clúster, incluyendo información como certificados y llaves privadas.
- **Estructura:**
  ```yaml
  users:
  - name: nombre-del-usuario
    user:
      client-certificate: ruta/al/certificado.pem
      client-key: ruta/al/llave-privada.pem
  ```
- **Explicación:**
  - **name:** Nombre descriptivo del usuario.
  - **user:**
    - **client-certificate:** Ruta al certificado del cliente para autenticación.
    - **client-key:** Ruta a la llave privada del cliente.

**Current-context:**
- **Definición:** El `current-context` en el kubeconfig de Kubernetes especifica el contexto actual, es decir, el conjunto de configuraciones (clúster y usuario) que `kubectl` utilizará por defecto.
- **Estructura:**
  ```yaml
  current-context: nombre-del-contexto
  ```
- **Explicación:**
  - **nombre-del-contexto:** Nombre del contexto que se establece como el actual para `kubectl`.

Estas configuraciones permiten organizar y gestionar eficientemente las interacciones con diferentes clústeres y usuarios en entornos de Kubernetes.

### Configuración adicional:

Además de estos componentes clave, el kubeconfig también puede contener configuraciones adicionales, como opciones de proxy, configuraciones de nombres de espacios (`namespaces`), entre otras.

### Ejemplo práctico:

```yaml
apiVersion: v1
kind: Config
clusters:
- name: mi-cluster
  cluster:
    server: https://mi-cluster-api-server
    certificate-authority: /ruta/al/authority.pem
contexts:
- name: mi-contexto
  context:
    cluster: mi-cluster
    user: mi-usuario
current-context: mi-contexto
users:
- name: mi-usuario
  user:
    client-certificate: /ruta/al/certificado.pem
    client-key: /ruta/al/llave-privada.pem
```

En este ejemplo:

- `mi-cluster` es el nombre del clúster.
- `mi-contexto` es el nombre del contexto que combina el clúster y el usuario.
- `mi-usuario` es el nombre del usuario con su respectivo certificado y llave privada.

Estos valores pueden variar según tu entorno específico de Kubernetes. Al configurar `kubectl`, es común modificar este archivo o tener varios kubeconfigs para diferentes entornos o proyectos.

---

## Comandos

#### Cambiar el contexto actual:

El comando `kubectl config use-context clusterDESA` se utiliza para cambiar el contexto actual en tu configuración de kubeconfig a "clusterDESA". Un contexto en Kubernetes es una combinación de clúster, espacio de nombres y usuario que define el entorno en el que se ejecutarán los comandos de kubectl.

* Aquí está el desglose del comando:

```bash
kubectl config use-context clusterDESA
```

- `kubectl config`: Es el comando para gestionar la configuración de kubectl.
- `use-context`: Es la subcomando que se utiliza para cambiar al contexto especificado.
- `clusterDESA`: Es el nombre del contexto al que deseas cambiar.

Este comando cambiará el contexto actual de tu configuración de kubectl al contexto llamado "clusterDESA", lo que significa que todos los comandos que ejecutes posteriormente utilizarán la configuración (clúster, espacio de nombres, usuario, etc.) asociada con ese contexto. Esto es útil cuando necesitas cambiar entre diferentes entornos o clústeres en Kubernetes.

#### Agregar un nuevo cluster:

El comando `kubectl config set-cluster cluster2 --server=https://1.2.3.4` se utiliza para definir o actualizar la configuración de un clúster en tu archivo de configuración kubeconfig. Aquí está el desglose del comando:

```bash
kubectl config set-cluster cluster2 --server=https://1.2.3.4
```

- `kubectl config`: Es el comando para gestionar la configuración de kubectl.
- `set-cluster`: Es la subcomando que se utiliza para definir o actualizar la configuración de un clúster.
- `cluster2`: Es el nombre que le estás dando al clúster. Puedes elegir cualquier nombre descriptivo.
- `--server=https://1.2.3.4`: Especifica la dirección del servidor de la API del clúster. En este caso, se establece en `https://1.2.3.4`.

Este comando establecerá la configuración del clúster llamado "cluster2" en tu archivo de configuración kubeconfig, con el servidor de la API configurado en `https://1.2.3.4`. Esto te permitirá interactuar con ese clúster utilizando el nombre "cluster2" en lugar de la URL completa del servidor de la API.

#### Agregar un nuevo cluster en un archivo kubeconfig diferente:

El comando `kubectl --kubeconfig=config_alter config set-cluster cluster2 --server=https://1.2.3.4` es similar al comando anterior, pero se usa para configurar un clúster específico en un archivo kubeconfig diferente al predeterminado. Aquí está el desglose del comando:

```bash
kubectl --kubeconfig=config_alter config set-cluster cluster2 --server=https://1.2.3.4
```

- `kubectl --kubeconfig=config_alter`: Esto indica que el comando `kubectl` utilizará el archivo kubeconfig llamado "config_alter" en lugar del archivo kubeconfig predeterminado.
- `config`: Este es el nombre del archivo kubeconfig que se utilizará.
- `set-cluster`: Es la subcomando que se utiliza para definir o actualizar la configuración de un clúster.
- `cluster2`: Es el nombre que le estás dando al clúster. Puedes elegir cualquier nombre descriptivo.
- `--server=https://1.2.3.4`: Especifica la dirección del servidor de la API del clúster. En este caso, se establece en `https://1.2.3.4`.

Este comando establecerá la configuración del clúster llamado "cluster2" en el archivo kubeconfig "config_alter", con el servidor de la API configurado en `https://1.2.3.4`. Esto te permitirá interactuar con ese clúster utilizando el nombre "cluster2" en el archivo kubeconfig específico.

#### Agregar un nuevo usuario:

El comando `kubectl config set-credentials usu1 --username=usu1 --password=c2VjcmV0Cg== --client-certificate=/home/dev1/fichero.crt --client-key=/home/dev1/fichero.key` se utiliza para definir o actualizar las credenciales de un usuario en tu archivo de configuración kubeconfig. Aquí está el desglose del comando:

```bash
kubectl config set-credentials usu1 --username=usu1 --password=c2VjcmV0Cg== --client-certificate=/home/dev1/fichero.crt --client-key=/home/dev1/fichero.key
```

- `kubectl config`: Es el comando para gestionar la configuración de kubectl.
- `set-credentials`: Es la subcomando que se utiliza para definir o actualizar las credenciales de un usuario.
- `usu1`: Es el nombre que le estás dando al usuario. Puedes elegir cualquier nombre descriptivo.
- `--username=usu1`: Especifica el nombre de usuario para el usuario.
- `--password=c2VjcmV0Cg==`: Especifica la contraseña para el usuario. En este caso, parece ser una contraseña codificada en Base64.
- `--client-certificate=/home/dev1/fichero.crt`: Especifica la ruta al certificado de cliente asociado con el usuario.
- `--client-key=/home/dev1/fichero.key`: Especifica la ruta a la clave de cliente asociada con el usuario.

Este comando establecerá la configuración de credenciales para el usuario llamado "usu1" en tu archivo de configuración kubeconfig. Estas credenciales se utilizarán para autenticar al usuario cuando se conecte al clúster. Es importante tener en cuenta que almacenar contraseñas en texto plano o codificadas en Base64 no es seguro, y se recomienda el uso de métodos más seguros de autenticación, como tokens o certificados.