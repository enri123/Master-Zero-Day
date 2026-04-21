Continuando el ejemplo anterior, usando dir, obtenemos los dos plugins de wordpress
![[Pasted image 20260329170202.png]]

![[Pasted image 20260329170216.png]]
Buscamos el exploit para esa versión del plugin Canto
![[Pasted image 20260329170242.png]]

Clonamos el exploit de github
![[Pasted image 20260329170404.png]]

Copiamos el php de pentestmonkey
![[Pasted image 20260329170451.png]]

Cambiamos la ip y el puerto de escucha, para poner los nuestros
![[Pasted image 20260329170503.png]]

Ejecutamos el exploit, en -u ponemos la maquina objetivo, en LHOST, nuestra maquina local y en NC_PORT, el puerto por el que estamos escuchando
![[Pasted image 20260329170619.png]]
Nos da error debido a que no tenemos instalado ni el requests, ni python
![[Pasted image 20260329170629.png]]
![[Pasted image 20260329170636.png]]
![[Pasted image 20260329170658.png]]
Ya hemos conseguido acceder a la maquina objetivo
![[Pasted image 20260329170713.png]]

