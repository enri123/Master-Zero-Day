![[Pasted image 20260311161521.png]]

![[Pasted image 20260311161558.png]]
ç

![[Pasted image 20260311161631.png]]

 ![[Pasted image 20260311162621.png]]

Creamos las variables globales, **INTERFAZ** la interfaz de red que queremos escuchar, en este caso eth0, **ARCHIVO_DUMP** el fichero donde queremos enviar los datos obtenidos y **PUERTO_HTTP** el puerto donde queremos activar el servidor, en este caso 80
![[Pasted image 20260311162928.png]]

Le pasamos a la función tcpdump el nombre de la interfaz y el archivo donde tiene que escribir, y le ponemos & para que se ejecute en segundo plano, tras 5 segundo encendemos el servidor, también en segundo plano, esperamos 30 segundos, en un uso real debería ser mucho mas, obtenemos el numero de los procesos con pgrep y posteriormente los eliminamos