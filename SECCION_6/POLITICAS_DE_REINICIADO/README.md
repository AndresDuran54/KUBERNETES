# Políticas de reiniciado en kubernetes

En Kubernetes, puedes controlar cómo se manejan los reinicios de los pods utilizando políticas de reinicio. A continuación, te menciono algunas de las políticas de reinicio más comunes:

## Always
Esta es la política de reinicio predeterminada en Kubernetes. Si se establece esta política, Kubernetes intentará reiniciar el pod cada vez que falle. Esto significa que si un pod falla o termina por cualquier motivo, Kubernetes intentará crear un nuevo pod para reemplazarlo inmediatamente. Ejemplo:
``` yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: tomcat
    labels:
        app: tomcat
    spec:
    containers:
        - name: tomcat     
            image: tomcat
    restartPolicy: Always
```

## OnFailure
Con esta política, Kubernetes solo intentará reiniciar el pod si el pod falla, es decir, si su proceso principal termina con un código de salida diferente de cero. Ejemplo:
``` yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: tomcat
    labels:
        app: tomcat
    spec:
    containers:
        - name: tomcat     
            image: tomcat
    restartPolicy: OnFailure
```

## Never
Esta política significa que Kubernetes nunca intentará reiniciar el pod automáticamente. Si el pod falla o se detiene, debe ser reiniciado manualmente por un administrador o un proceso externo. Ejemplo:
``` yaml
    apiVersion: v1
    kind: Pod
    metadata:
    name: tomcat
    labels:
        app: tomcat
    spec:
    containers:
        - name: tomcat     
            image: tomcat
    restartPolicy: Never
```

# Estados de un Pod en Kubernetes

En Kubernetes, un pod puede experimentar varios estados a lo largo de su ciclo de vida. Los estados principales que puede tener un pod son los siguientes:

1. **Pending (Pendiente)**: Cuando se crea un pod, primero entra en el estado "Pending". Esto significa que Kubernetes está en proceso de asignar recursos a este pod y programarlo para su ejecución en un nodo. El pod permanece en este estado hasta que todos los recursos necesarios están disponibles.

2. **Running (Ejecutando)**: Un pod entra en el estado "Running" cuando todos sus contenedores han sido programados en un nodo y están en ejecución. En este estado, los contenedores dentro del pod están funcionando y listos para procesar solicitudes.

3. **Succeeded (Completado)**: Un pod entra en el estado "Succeeded" cuando todos sus contenedores se ejecutan exitosamente y luego se detienen. Esto es común en tareas de un solo uso o trabajos que se ejecutan hasta su finalización.

4. **Failed (Fallido)**: Si uno o más contenedores dentro de un pod terminan con un error o no pueden iniciarse, el pod entra en el estado "Failed". Esto indica que algo salió mal en la ejecución de los contenedores.

5. **Unknown (Desconocido)**: El estado "Unknown" se utiliza cuando Kubernetes no puede obtener información sobre el estado real del pod. Esto podría deberse a problemas de comunicación con el nodo o con el contenedor.

6. **Terminating (Terminando)**: Cuando se elimina un pod, entra en el estado "Terminating". Esto significa que Kubernetes está en proceso de eliminar todos los contenedores del pod y liberar los recursos asociados. Una vez que se completa este proceso, el pod se elimina por completo.

7. **ContainerCreating (Creando contenedor)**: Este es un estado intermedio que indica que Kubernetes está en proceso de crear los contenedores del pod, pero aún no están en ejecución.

8. **CrashLoopBackOff (Ciclo de caída y reinicio)**: Si un pod entra en un ciclo de reinicio continuo debido a un error recurrente en uno o más de sus contenedores, puede quedar atrapado en el estado "CrashLoopBackOff".

Estos son los estados principales que un pod puede experimentar en Kubernetes. Es importante monitorear y gestionar los pods para garantizar que estén en el estado deseado y funcionando correctamente según las necesidades de tu aplicación.
