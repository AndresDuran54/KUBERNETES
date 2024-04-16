# Montar un servidor NFS

Necesitamos un HOST maestro y un HOST esclavo.

### Configuración en el HOST maestro

#### 1. Instalamos en el HOST lo siguiente

```bash
    apt-get install nfs-kernel-server
```

#### 2. Crear un directorio, donde se guardaran los datos compartidos de todos los nodos

```bash
    mkdir /var/datos
```

#### 3. Editar dichero /etc/exports, agregando la siguiente linea

```bash
    /var/datos *(rw,sync,no_root_squash,no_all_squash)
```

#### 4. Reiniciamos el NFS

```bash
    systemctl restart nfs-kernel-server
```

#### 5. Ejecutamos el siguiente comando para ver si está todo correcto

```bash
    showmount -e $IP_LOCAL_MAESTRO
```

### Configuración en el HOST esclavo

#### 1. En el nodo worker instalar:

```bash
    apt-get install nfs-common
```

#### 2. Ejecutamos el siguiente comando para ver si está todo correcto

```bash
    showmount -e $IP_LOCAL_MAESTRO
```

#### 3. Crear un directorio, para sincronizar con la carpeta del nodo maestro

```bash
    mkdir /var/datos
```

### 4. Montamos la carpeta del maestro al esclavo

```bash
    mount -t nfs $IP_LOCAL_MAESTRO:/var/datos /var/datos
```