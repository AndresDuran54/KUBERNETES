

Pasos;

1. En el nodo maestro y en los nodos esclavos creamos las carpetas

/home/kubernetes/datos/mysql
/home/kubernetes/datos/wordpress

2. Luego en el nodo maestro en el archivo /etc/exports, agregamos las siguientes lineas:
   
/home/kubernetes/datos/mysql *(rw,sync,no_noot_squash,no_all_squash)
/home/kubernetes/datos/wordpress *(rw,sync,no_noot_squash,no_all_squash)

3. Luego reiniciamos el kernel del nfs

systemctl restart nfs-kernel-server

4. En el nodo esclavo 1

mount -t nfs $IP_LOCAL_MAESTRO:/home/kubernetes/datos/wordpress /home/kubernetes/datos/wordpress
mount -t nfs $IP_LOCAL_MAESTRO:/home/kubernetes/datos/mysql /home/kubernetes/datos/mysql
