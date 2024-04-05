# Priority Class

Las Priority Classes (clases de prioridad) son un mecanismo en Kubernetes que se utiliza para asignar prioridades a los Pods dentro de un clúster. Permiten controlar el orden en que los Pods son programados y cuáles tienen acceso a los recursos en situaciones de escasez.

Aquí hay algunos aspectos importantes sobre las Priority Classes en Kubernetes:

1. **Asignación de prioridades**: Las Priority Classes asignan un valor numérico que representa la prioridad relativa de los Pods. Cuanto mayor sea el valor numérico, mayor será la prioridad del Pod.

2. **Conflictos de prioridad**: Si hay múltiples Pods compitiendo por los mismos recursos y no hay suficientes recursos disponibles para todos, Kubernetes utilizará las Priority Classes para resolver los conflictos. Los Pods con una Priority Class más alta tendrán prioridad sobre los Pods con una Priority Class más baja.

3. **Default Priority Class**: Kubernetes tiene una Priority Class predeterminada que se asigna a todos los Pods que no tienen una Priority Class explícitamente definida. Esta Priority Class predeterminada suele tener un valor bajo, lo que significa que los Pods sin prioridad explícita tendrán una prioridad más baja en comparación con los que tienen una Priority Class definida.

4. **Uso con Quality of Service (QoS)**: Las Priority Classes pueden utilizarse junto con Quality of Service (QoS) para controlar el comportamiento de planificación y escalabilidad de los Pods. Por ejemplo, los Pods con una Priority Class alta y una clase de servicio "Guaranteed" tendrán prioridad máxima y recibirán garantías de recursos.

En resumen, las Priority Classes son una herramienta importante en Kubernetes para controlar la prioridad de los Pods y garantizar que los recursos se asignen de manera efectiva en situaciones de escasez. Permiten gestionar mejor la planificación y el rendimiento de los Pods dentro del clúster.

### Clausula preemptionPolicy

En los objetos PriorityClass de Kubernetes, la propiedad `preemptionPolicy` define cómo se manejará la prelación de los Pods cuando los recursos sean escasos. Hay dos valores posibles para esta propiedad:

1. **PreemptLowerPriority**: Esta política permite que los Pods con prioridades más altas desplacen (o expulsen) los Pods con prioridades más bajas cuando se necesita liberar recursos para acomodar los Pods de alta prioridad.

2. **NeverPreempt**: Esta política indica que los Pods con una prioridad específica nunca serán expulsados para dar paso a Pods con prioridades más altas. Esto significa que los Pods de esta prioridad se consideran inamovibles y permanecerán en ejecución incluso si la capacidad de recursos es insuficiente.

Estas políticas son útiles para controlar el comportamiento de prelación en un clúster de Kubernetes y asegurar que los recursos estén disponibles para los Pods más importantes según sus prioridades asignadas.