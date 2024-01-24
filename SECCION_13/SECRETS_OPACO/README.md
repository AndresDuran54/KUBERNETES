## Comando: Crear un Secreto en Kubernetes

El siguiente comando `kubectl` se utiliza para crear un secreto en Kubernetes llamado "passwords" que contiene dos literales con claves y contraseñas asociadas:

```bash
kubectl create secret generic passwords --from-literal=pass-root=kubernetes --from-literal=pass-usu=kubernetes
```

- `create secret generic passwords`: Esta parte del comando indica que se está creando un secreto genérico llamado "passwords". Este tipo de secreto se utiliza para almacenar datos sensibles, como contraseñas.

- `--from-literal=pass-root=kubernetes`: Aquí se especifica que se está añadiendo un literal al secreto con la clave "pass-root" y el valor "kubernetes". Este literal representa una contraseña asociada a la clave "pass-root".

- `--from-literal=pass-usu=kubernetes`: Similar al anterior, se añade otro literal al secreto con la clave "pass-usu" y el valor "kubernetes", representando otra contraseña asociada a la clave "pass-usu".

Este comando es útil para almacenar contraseñas de manera segura en Kubernetes, y los secretos creados pueden ser utilizados por aplicaciones y servicios que necesitan acceder a información confidencial.