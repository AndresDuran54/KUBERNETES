# Sección 6

## Crear una imagen Docker

Para crear una imagen Docker, utiliza el comando `docker build` seguido de la ruta al directorio que contiene los archivos necesarios. Además, especifica el nombre y la etiqueta que deseas asignar a la imagen con la opción `-t`.

```bash
docker build SECCION_6/CREAR_POD_YAML/ -t andresduran54/nginx:v1
```

## Ejecutar un contenedor Docker con NGINX

Para ejecutar un contenedor Docker utilizando la imagen `andresduran54/nginx:v1` de NGINX, utiliza el comando `docker run`. A continuación, se detallan las opciones utilizadas en el comando:

- `-d`: Esta opción ejecuta el contenedor en segundo plano (modo detached).
- `-p 80:80`: Esta opción mapea el puerto 80 del host al puerto 80 del contenedor, permitiendo el acceso al servicio NGINX.
- `--name nginx`: Esta opción asigna el nombre "nginx" al contenedor.
- `andresduran54/nginx:v1`: Especifica la imagen que se utilizará para crear el contenedor.

```bash
docker run -d -p 80:80 --name nginx andresduran54/nginx:v1
```

## Comando: Exponer un Pod en Kubernetes

El comando `kubectl expose` se utiliza para exponer recursos en Kubernetes, como pods, como servicios de red accesibles desde fuera del clúster.

- `kubectl expose pod nginx`: Este es el comando base para exponer un pod llamado "nginx". Indica que quieres crear un servicio para acceder a ese pod.

- `--name=nginx-svc`: Con esta opción, estás proporcionando un nombre personalizado para el servicio que se creará. En este caso, el nombre del servicio se establecerá como "nginx-svc".

- `--port=80`: Con esta opción, estás especificando el puerto en el que el servicio estará escuchando. Aquí se establece el puerto 80, que es un puerto común para tráfico HTTP.

- `--type=LoadBalancer`: Esta opción define el tipo de servicio que se creará. En este caso, estás indicando que el servicio debe ser de tipo "LoadBalancer". Un servicio LoadBalancer permite exponer el pod a través de un balanceador de carga externo, lo que es útil para distribuir el tráfico de manera equitativa entre varios pods.

```bash
kubectl expose pod nginx --name=nginx-svc --port=80 --type=LoadBalancer
```

## Comando: Obtener Detalles de un Pod en Formato YAML

El comando `kubectl get pod/nginx -o yaml` se utiliza en Kubernetes para obtener los detalles de un pod específico en el formato YAML. Aquí está la desglose del comando:

- `kubectl get pod/nginx`: Con esta parte del comando, estás solicitando información sobre el pod llamado "nginx". El prefijo `pod/` indica que estás buscando un recurso de tipo pod.

- `-o yaml`: Esta opción indica que deseas que la salida se formatee en YAML. YAML es un formato legible por humanos que se utiliza comúnmente para definir configuraciones en Kubernetes. También le podríamos pasar la opción `json`

En resumen, el comando `kubectl get pod/nginx -o yaml` te proporcionará un resultado en formato YAML que contiene los detalles del pod "nginx", como su estado actual, las etiquetas asociadas, el espacio de nombres, la dirección IP asignada y otros metadatos relacionados con el pod.

Recuerda que el formato YAML es utilizado para representar estructuras de datos en Kubernetes, lo que facilita la lectura y comprensión de la configuración y el estado de los recursos en el clúster.

```bash
kubectl get pod/nginx -o yaml
```
