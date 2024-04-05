# Unidades de medida de recursos

En Kubernetes, las unidades de medida de recursos para CPU y memoria se pueden expresar de diferentes maneras. Aquí tienes algunas opciones comunes:

### Unidades de memoria:
- **Mi:** Megabytes
- **Gi:** Gigabytes
- **Ki:** Kilobytes
- **Ti:** Terabytes
- **K:** 1,000 bytes
- **M:** 1,000,000 bytes
- **G:** 1,000,000,000 bytes
- **T:** 1,000,000,000,000 bytes

### Unidades de CPU:
- **m:** Milicores (1/1000 de un núcleo)
- **n:** Núcleos

Por ejemplo, para especificar 512 Megabytes de memoria, puedes usar `"512Mi"`. Para 0.5 núcleos de CPU, puedes usar `"500m"`. Estas son las convenciones más comunes, pero también puedes usar otras unidades de medida según tus necesidades.