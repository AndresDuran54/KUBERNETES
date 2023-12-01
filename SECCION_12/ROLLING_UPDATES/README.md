## Rolling Updates en Kubernetes

**Rolling Updates** (Actualizaciones Graduales) es un enfoque de implementación en Kubernetes que permite actualizar una aplicación de manera incremental y controlada sin causar interrupciones en el servicio. Este método se utiliza comúnmente al actualizar despliegues para garantizar la disponibilidad continua de la aplicación.

### Tipos:

1. **Rolling Update (Actualización Gradual):**

   Descripción: Esta estrategia actualiza los pods de manera gradual, reemplazando progresivamente los pods antiguos con los nuevos. Garantiza la disponibilidad continua de la aplicación durante el proceso de actualización.

2. **Recreate (Recrear):**

   Descripción: Esta estrategia elimina todos los pods existentes antes de crear los nuevos. Durante el proceso, la aplicación puede experimentar un breve período de inactividad.


### Características Clave:

1. **Implementación Incremental:**
   - En una actualización gradual, los nuevos pods se implementan de manera incremental mientras los pods antiguos aún están en ejecución. Esto asegura que la aplicación esté disponible durante todo el proceso de actualización.

2. **Control de la Velocidad de Actualización:**
   - Puedes controlar la velocidad de la actualización especificando parámetros como el número máximo de pods que se pueden actualizar simultáneamente y el período de espera entre actualizaciones.

3. **Monitoreo de Salud:**
   - Kubernetes monitorea la salud de los nuevos pods antes de continuar con la actualización. Si un nuevo pod no se inicia correctamente o no pasa las comprobaciones de salud, Kubernetes puede detener la actualización para evitar la degradación del servicio.

4. **Rollback Automático:**
   - Si se detectan problemas durante la actualización, Kubernetes puede realizar un rollback automáticamente a la versión anterior del despliegue para garantizar la continuidad del servicio.

5. **Versión de Despliegue:**
   - En un despliegue de tipo Rolling Update, puedes especificar la versión de la imagen del contenedor que se utilizará para los nuevos pods. Esto permite una actualización controlada de la aplicación.

### Ejemplo de Uso:

Un ejemplo de uso de Rolling Updates es la actualización de una aplicación web sin que los usuarios experimenten tiempos de inactividad. Kubernetes realiza la transición entre versiones gradualmente, dirigiendo el tráfico hacia los nuevos pods a medida que se confirma su salud y retirando los pods antiguos de manera segura.

Para implementar un Rolling Update en Kubernetes, generalmente se utiliza el comando `kubectl apply` o `kubectl set image` para actualizar la definición del despliegue con la nueva versión de la imagen del contenedor.

## Comando: Ver Detalles de una Revisión Específica en el Historial de Implementación

El comando `kubectl rollout history deploy nginx-d --revision=1` se utiliza en Kubernetes para obtener detalles específicos de una revisión particular en el historial de implementación de un despliegue llamado "nginx-d".

**Descripción:**

- `kubectl rollout history deploy nginx-d --revision=1`: Esta parte del comando indica que deseas ver los detalles de la revisión número 1 en el historial de implementación del despliegue "nginx-d".

Este comando te proporcionará información detallada sobre los cambios realizados en la revisión especificada, permitiéndote analizar los detalles específicos de esa implementación en particular.

Es útil cuando necesitas revisar los cambios realizados en una versión anterior del despliegue o si deseas entender mejor los eventos asociados con una revisión específica.

Si tienes más preguntas o necesitas más información, no dudes en preguntar.

## Comando: Verificar el Estado de la Actualización de un Despliegue en Kubernetes

El comando `kubectl rollout status deploy nginx-d` se utiliza en Kubernetes para verificar el estado de la actualización de un despliegue específico llamado "nginx-d".

**Ejemplo de Salida:**
```
Waiting for deployment "nginx-d" rollout to finish: 9 out of 10 new replicas have been updated...
deployment "nginx-d" successfully rolled out
```

- La primera línea indica que está esperando a que la implementación "nginx-d" termine su actualización. En este ejemplo, muestra que se han actualizado 9 de las 10 réplicas planificadas.

- La segunda línea indica que la implementación "nginx-d" se ha implementado correctamente.

Este comando proporciona una visión rápida del progreso de la actualización y si se ha completado con éxito. Puedes utilizarlo para monitorear la finalización de una actualización de manera interactiva.

Recuerda que este comando espera a que la implementación termine, por lo que podría bloquear la terminal. Si deseas ejecutarlo en segundo plano, puedes agregar el flag `-w` o `--watch`:

```bash
kubectl rollout status deploy nginx-d -w
```

## Comando: Deshacer una Actualización en Kubernetes

El comando `kubectl rollout undo deploy nginx-d --to-revision=4` se utiliza en Kubernetes para revertir una implementación a una revisión específica del despliegue llamado "nginx-d". Este comando deshace la actualización, volviendo al estado de la implementación en la revisión especificada.

**Parámetros:**
- `undo deploy nginx-d`: Indica que deseas deshacer la implementación del despliegue llamado "nginx-d".
- `--to-revision=4`: Especifica la revisión a la cual deseas revertir la implementación. En este ejemplo, se revierte a la revisión número 4.

Este comando es útil cuando necesitas realizar un rollback a una versión anterior del despliegue debido a problemas detectados después de una actualización.

Recuerda que deshacer una actualización puede afectar la disponibilidad de la aplicación durante el proceso de rollback.


