Descargamos Logan
![[Pasted image 20260320114240.png]]
![[Pasted image 20260320114302.png]]

Escaneamos las maquinas en nuestra red local
![[Pasted image 20260320114339.png]]

Escaneamos los puertos abiertos con nmap
![[Pasted image 20260320114614.png]]

Para que nos funcione tenemos en nuestro etc/hosts poner la ip de la maquina objetivo con su dominio
![[Pasted image 20260320114721.png]]
![[Pasted image 20260320114738.png]]

hacemos un wfuzz, filtramos para que no nos muestre los que den error 404, ponemos una wordlist con -w y el host y la ip con -H y -u
![[Pasted image 20260320114945.png]]
![[Pasted image 20260320115151.png]]
![[Pasted image 20260320115205.png]]

Ocultamos tambien los archivos que solo tienen  una linea de texto
![[Pasted image 20260320115249.png]]

Para poder acceder a los subdominios tenemos ue agregarlos en el etc/hosts
![[Pasted image 20260320115322.png]]




