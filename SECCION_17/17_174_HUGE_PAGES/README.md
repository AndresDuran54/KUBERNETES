# HubePages

Los "HugePages" en Kubernetes se refieren a una funcionalidad del sistema operativo que permite gestionar grandes bloques de memoria física de manera más eficiente. Estos bloques de memoria se utilizan principalmente para aplicaciones que requieren un gran espacio de memoria, como bases de datos en memoria, procesos intensivos en memoria, entre otros.

En el contexto de Kubernetes, puedes configurar el uso de HugePages para tus contenedores si necesitas gestionar grandes cantidades de memoria de manera eficiente. Esto se puede hacer configurando adecuadamente los recursos de los contenedores y los límites de recursos en Kubernetes.

El uso de HugePages puede mejorar el rendimiento y la eficiencia de las aplicaciones que requieren grandes cantidades de memoria al reducir la fragmentación de la memoria y mejorar la utilización de los recursos físicos del sistema. Sin embargo, es importante tener en cuenta que la configuración y el uso de HugePages deben realizarse cuidadosamente, ya que pueden tener un impacto significativo en el rendimiento y la estabilidad del sistema.

### Ejemplo real

Un ejemplo real de cuándo sería óptimo usar HugePages en Kubernetes sería en el caso de ejecutar una base de datos en memoria, como Redis o Memcached, que requiera grandes cantidades de memoria RAM para almacenar datos en caché de manera eficiente.

Estas bases de datos suelen trabajar con conjuntos de datos muy grandes que necesitan ser almacenados en memoria para un acceso rápido. Al utilizar HugePages, se pueden asignar bloques de memoria grandes y contiguos, lo que reduce la fragmentación de la memoria y mejora el rendimiento general de la base de datos.

Por ejemplo, si tienes un clúster de Kubernetes que ejecuta una aplicación de análisis en tiempo real que requiere Redis para almacenar cachés de datos, configurar HugePages puede ser beneficioso para garantizar un rendimiento óptimo de Redis y la aplicación en general.

En resumen, el uso de HugePages en Kubernetes puede ser óptimo en situaciones donde se requiere un acceso rápido a grandes conjuntos de datos en memoria, como en bases de datos en memoria o aplicaciones de análisis en tiempo real.

### Cómo establecer un número de HugePages en Linux

#### 1. Consultamos el tamaño de HugePage que soporta nuestro sistema operativo

```bash
    cat /proc/meminfo
```

El archivo `/proc/meminfo` proporciona información detallada sobre el estado de la memoria del sistema en Linux. Contiene información sobre la memoria física, la memoria swap y otros aspectos relacionados con la memoria del sistema. Aquí hay un resumen de la información que generalmente se encuentra en este archivo:

1. **Memoria física (RAM)**:
   - MemTotal: La cantidad total de memoria física disponible en el sistema.
   - MemFree: La cantidad de memoria física que actualmente está disponible para su uso.
   - MemAvailable: Una estimación de la cantidad de memoria física que está disponible para su uso por los procesos del sistema.
   - Buffers: La cantidad de memoria utilizada como buffers para E/S de disco.
   - Cached: La cantidad de memoria utilizada como caché de página.
   - SwapCached: La cantidad de memoria swap que está actualmente en caché.
   - Active: La cantidad de memoria actualmente en uso o marcada como activa.
   - Inactive: La cantidad de memoria que no ha sido accedida recientemente y se puede reutilizar.
   - Shmem: La cantidad de memoria compartida anónima.
   - Slab: La cantidad de memoria en uso por el kernel para almacenar estructuras de datos.
   - SReclaimable: La cantidad de memoria en el caché de slab que se puede reclamar (por ejemplo, caché de inode y dentry).
   - SUnreclaim: La cantidad de memoria en el caché de slab que no se puede reclamar.
   - KernelStack: La cantidad de memoria utilizada por los stacks del kernel.
   - HugePages_Total: Este campo indica el número total de hugepages disponibles en el sistema.
   - HugePages_Free: Indica el número de hugepages que están actualmente libres y disponibles para su   asignación.
   - HugePages_Rsvd: Este campo muestra el número de hugepages que están reservadas para el sistema, pero que no están actualmente en uso.
   - HugePages_Surp: Indica el número de hugepages que están en exceso. Estos son hugepages que no se pudieron reservar debido a la fragmentación de la memoria o a otros problemas.
   - Hugepagesize: Tamaño de los HugePage que soporta el S.O

1. **Memoria swap**:
   - SwapTotal: La cantidad total de espacio de intercambio disponible en el sistema.
   - SwapFree: La cantidad de espacio de intercambio que actualmente está disponible para su uso.

Además de estos, hay otros campos que proporcionan información adicional sobre la memoria del sistema. Cada campo suele estar acompañado de su unidad de medida correspondiente (kilobytes, megabytes, etc.). Este archivo es una herramienta útil para monitorear el estado de la memoria del sistema en tiempo real y para diagnosticar problemas relacionados con la memoria. Puedes ver el contenido del archivo utilizando el comando `cat /proc/meminfo`.

En este caso nos interesa el campo Hugepagesize que nos indica el tamaño de cada HugePage que sorpote nuestro sistema operativo.

#### 2. Configurar el número de HugePages

El archivo `/etc/sysctl.conf` es un archivo de configuración en sistemas Linux que se utiliza para configurar parámetros del kernel en el arranque del sistema. Estos parámetros controlan diversos aspectos del funcionamiento del kernel y del sistema en general. Aquí hay un resumen de lo que puedes encontrar en este archivo:

1. **Configuración del kernel**: Puedes establecer y modificar varios parámetros del kernel, como la gestión de la memoria, el manejo de la red, la seguridad, la virtualización y otros aspectos del sistema. Por ejemplo, puedes ajustar el tamaño del búfer de red, habilitar o deshabilitar la protección contra ataques de denegación de servicio (DoS), o configurar la protección de memoria del kernel.

2. **Configuración de red**: Puedes configurar parámetros relacionados con el funcionamiento de la red, como el enrutamiento IP, la velocidad de la conexión, el límite de conexiones, la retransmisión de paquetes, entre otros.

3. **Configuración de seguridad**: Puedes ajustar parámetros de seguridad del sistema, como el control de acceso, la protección contra ataques, la gestión de procesos, entre otros.

4. **Optimización del rendimiento**: Puedes configurar parámetros para optimizar el rendimiento del sistema, como el manejo de la memoria, el uso de la CPU, la gestión de E/S, entre otros.

Es importante tener en cuenta que los cambios realizados en este archivo afectan la configuración del kernel y, por lo tanto, pueden tener un impacto significativo en el funcionamiento del sistema. Es recomendable tener un buen entendimiento de los parámetros que se están modificando y sus implicaciones antes de realizar cambios en este archivo. Además, es posible que algunos cambios requieran reiniciar el sistema para que surtan efecto.

La configuración `vm.nr_hugepages=100` en el archivo `/etc/sysctl.conf` se refiere al número de páginas enormes (hugepages) reservadas para el sistema. 

Las páginas enormes son un mecanismo en el kernel de Linux que permite asignar grandes bloques de memoria física contigua para mejorar el rendimiento en aplicaciones que manejan grandes conjuntos de datos, como bases de datos en memoria, servidores de aplicaciones, o aplicaciones de procesamiento intensivo. Al asignar memoria en bloques más grandes, se reduce la sobrecarga del sistema operativo asociada con la gestión de muchas páginas de tamaño estándar.

La configuración `vm.nr_hugepages=100` establece el número de páginas enormes en 100. Esto significa que se reservarán 100 páginas enormes para el sistema. El tamaño exacto de cada página enorme depende de la configuración del sistema y del hardware, pero generalmente es mucho mayor que el tamaño de una página estándar. 

Es importante tener en cuenta que el número de páginas enormes y su tamaño se deben ajustar cuidadosamente según las necesidades específicas de la aplicación y el hardware del sistema. Un número inadecuado de páginas enormes o un tamaño incorrecto pueden tener un impacto negativo en el rendimiento del sistema. Por lo tanto, se recomienda realizar pruebas exhaustivas antes de modificar esta configuración en un entorno de producción.

#### 3. Obtener el tamaño de cada página de memoria de mi sistema

El comando `getconf PAGESIZE` consulta la configuración del sistema para obtener el tamaño de las páginas de memoria en bytes. Este valor representa el tamaño de las páginas de memoria convencionales en el sistema.

Cuando ejecutas `getconf PAGESIZE`, el sistema devuelve el tamaño de las páginas de memoria en bytes directamente desde el kernel, sin necesidad de leer un archivo específico.

Por lo tanto, puedes confiar en que el valor devuelto por `getconf PAGESIZE` representa con precisión el tamaño de las páginas de memoria en tu sistema.

#### 4. Actualizar la nueva configuración en el kernel

El comando `sudo sysctl -p` se utiliza en sistemas Linux para recargar la configuración del kernel desde el archivo de configuración `/etc/sysctl.conf`. Este archivo contiene configuraciones de kernel que se aplican durante el arranque del sistema, pero a veces es necesario recargar esta configuración sin reiniciar el sistema.

Cuando ejecutas `sudo sysctl -p`, el sistema lee el archivo `/etc/sysctl.conf` y aplica las configuraciones de kernel que contiene. Esto permite actualizar la configuración del kernel en tiempo de ejecución sin necesidad de reiniciar el sistema.

Es útil utilizar este comando después de realizar cambios en el archivo `/etc/sysctl.conf` para aplicar las nuevas configuraciones sin reiniciar el sistema.

# Con referencia al archivo de configuración

El campo `limits` en el recurso de `resources` dentro de la especificación de un contenedor en un Pod de Kubernetes se utiliza para establecer los límites máximos de recursos que el contenedor puede utilizar. En este caso, los campos `hugepages-2Mi` y `hugepages-1Gi` indican los límites de uso de páginas grandes de 2 MiB y 1 GiB, respectivamente.

Las páginas grandes son una característica del sistema de memoria de Linux que permite al kernel manejar grandes bloques de memoria de manera más eficiente que las páginas pequeñas convencionales. Estas páginas grandes pueden ser beneficiosas para aplicaciones que requieren un uso intensivo de memoria y pueden mejorar el rendimiento en ciertos escenarios.

En el ejemplo proporcionado, se establecen los siguientes límites de recursos para el contenedor:

- `hugepages-2Mi`: Se limita a un máximo de 100 MiB de uso de páginas grandes de 2 MiB.
- `hugepages-1Gi`: Se limita a un máximo de 2 GiB de uso de páginas grandes de 1 GiB.
- `memory`: Se limita a un máximo de 100 MiB de memoria convencional.
- `cpu`: Se limita a un máximo de 1 núcleo de CPU.

Estos límites garantizan que el contenedor no exceda los recursos especificados, lo que puede ser crucial para mantener el rendimiento y la estabilidad del sistema en un entorno Kubernetes.

En la sección de `volumes`, se definen los volúmenes que pueden montar los contenedores dentro del Pod. Cada volumen tiene un nombre único dentro del Pod y puede ser referenciado por los contenedores que lo necesiten.

En este caso, se definen dos volúmenes:

1. **`hugepage-2mi`**: Este volumen se configura como un `emptyDir`, lo que significa que es un directorio temporal compartido que existe mientras el Pod esté en ejecución. El campo `medium` indica que este directorio debe respaldarse con memoria de páginas grandes de 2 MiB (`HugePages-2Mi`). Esto permite que el contenedor acceda a este espacio de memoria optimizado para un rendimiento más eficiente en el uso de la memoria.

2. **`hugepage-1gi`**: Similar al anterior, este volumen también es un `emptyDir`, pero utiliza memoria de páginas grandes de 1 GiB (`HugePages-1Gi`) como medio de almacenamiento. Esto proporciona un espacio de memoria aún más grande y puede ser útil para aplicaciones que requieren una cantidad significativa de memoria y pueden beneficiarse de un uso eficiente de las páginas grandes.

En resumen, estos volúmenes están configurados para proporcionar a los contenedores acceso a espacios de memoria respaldados por páginas grandes, lo que puede ser beneficioso para aplicaciones con requisitos intensivos de memoria.

El campo `medium` dentro de la definición de un volumen en Kubernetes puede tomar diferentes valores, dependiendo de cómo se desee respaldar el almacenamiento del volumen. Algunos de los valores comunes que puede tomar `medium` son:

1. **`""` (cadena vacía)**: Este es el valor predeterminado y significa que se utilizará el medio de almacenamiento predeterminado del nodo, que generalmente es almacenamiento en disco local.

2. **`Memory`**: Indica que el volumen se respalda en la memoria RAM del nodo. Este tipo de volumen es útil cuando se necesitan volúmenes de almacenamiento rápidos y efímeros, ya que la memoria RAM es más rápida que el almacenamiento en disco, pero también se borra cuando el contenedor o el nodo se reinicia.

3. **Otros tipos de almacenamiento**: Dependiendo de la configuración específica de tu clúster Kubernetes y de los proveedores de almacenamiento que estés utilizando, es posible que haya otros valores disponibles para `medium`, como almacenamiento en red (NFS, Ceph, etc.) o almacenamiento en la nube (EBS, Azure Disk, etc.).

En resumen, el valor de `medium` en un volumen de Kubernetes indica dónde se almacenarán los datos del volumen y puede ser ajustado según los requisitos de la aplicación y las capacidades de almacenamiento disponibles en el clúster.