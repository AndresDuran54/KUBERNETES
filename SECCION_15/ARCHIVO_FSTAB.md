# /etc/fstab
El archivo `/etc/fstab` en Linux es un archivo de configuración que contiene información sobre los sistemas de archivos y otros dispositivos que deben montarse automáticamente en el arranque del sistema. El archivo `fstab` es fundamental para la administración de discos y particiones, ya que define cómo y dónde se montan los sistemas de archivos.

### Estructura del archivo `/etc/fstab`

El archivo `/etc/fstab` tiene un formato basado en columnas donde cada línea define un sistema de archivos. A continuación, se muestra un ejemplo típico de un archivo `fstab` y la explicación de cada campo:

```sh
# <file system>  <mount point>  <type>  <options>  <dump>  <pass>
UUID=1234-5678  /               ext4    defaults  1 1
UUID=8765-4321  /home           ext4    defaults  1 2
UUID=abcd-efgh  none            swap    sw        0 0
/dev/cdrom      /media/cdrom0   udf,iso9660 user,noauto,exec,utf8 0 0
```

### Campos del archivo `/etc/fstab`

1. **<file system>**: Identifica el sistema de archivos o dispositivo. Esto puede ser una partición (identificada por UUID o por el dispositivo, como `/dev/sda1`), un archivo de intercambio (`/swapfile`), o un recurso de red.
   
2. **<mount point>**: El punto de montaje en el sistema de archivos donde se montará el dispositivo. Por ejemplo, `/` para la raíz, `/home` para los directorios de usuario, y `none` para el swap.

3. **<type>**: El tipo de sistema de archivos, como `ext4`, `swap`, `ntfs`, `vfat`, etc.

4. **<options>**: Opciones de montaje que controlan el comportamiento del sistema de archivos. Ejemplos comunes incluyen `defaults`, `ro` (solo lectura), `rw` (lectura y escritura), `noexec` (no permitir la ejecución de binarios), y `nosuid` (no permitir el uso de `set-user-identifier` o `set-group-identifier`).

5. **<dump>**: Un número que indica si el sistema de archivos debe ser respaldado por el programa `dump`. Un valor de `0` significa que no se debe respaldar.

6. **<pass>**: Un número que indica el orden en el que los sistemas de archivos deben ser comprobados en el arranque por `fsck`. El valor `1` significa que el sistema de archivos debe ser comprobado primero (normalmente, la raíz), `2` significa que otros sistemas de archivos deben ser comprobados después, y `0` significa que no se debe comprobar.

### Ejemplo detallado

A continuación se presenta una línea de ejemplo y su explicación:

```sh
UUID=1234-5678  /               ext4    defaults  1 1
```

- **UUID=1234-5678**: El sistema de archivos está identificado por su UUID.
- **/**: El sistema de archivos se monta en la raíz.
- **ext4**: El tipo de sistema de archivos es ext4.
- **defaults**: Se utilizan las opciones de montaje por defecto (lectura y escritura, permitir ejecución, etc.).
- **1**: Se debe respaldar con `dump`.
- **1**: Se debe comprobar primero con `fsck`.

### Añadir una entrada para un archivo de intercambio

Si deseas añadir un archivo de intercambio al `fstab`, puedes hacerlo de la siguiente manera:

1. **Crear el archivo de intercambio** (si no lo has hecho ya):

    ```sh
    sudo fallocate -l 2G /swapfile
    sudo chmod 600 /swapfile
    sudo mkswap /swapfile
    sudo swapon /swapfile
    ```

2. **Añadir la entrada al `fstab`**:

    Edita el archivo `/etc/fstab` con un editor de texto (como `nano` o `vim`):

    ```sh
    sudo nano /etc/fstab
    ```

    Añade la siguiente línea al final del archivo:

    ```sh
    /swapfile none swap sw 0 0
    ```

### Resumen

El archivo `/etc/fstab` es esencial para la configuración y administración de los sistemas de archivos y dispositivos de almacenamiento en Linux. Define cómo y dónde se deben montar los sistemas de archivos durante el arranque, y permite personalizar las opciones de montaje para diferentes dispositivos.

Si tienes más preguntas o necesitas más detalles sobre cómo configurar `/etc/fstab`, ¡no dudes en preguntar!