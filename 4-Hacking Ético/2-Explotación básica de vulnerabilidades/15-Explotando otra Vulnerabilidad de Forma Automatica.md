Nos descargamos de DockerLabs la maquina chocolatefire.zip
![[Pasted image 20260318133622.png]]

Ejecutamos la maquina objetivo
![[Pasted image 20260318133647.png]]

Hacemos un escaneo de los puertos vulnerables
![[Pasted image 20260318133837.png]]
Puertos encontrados
![[Pasted image 20260318133847.png]]

En este caso nuestro puerto objetivo sera el 9090
![[Pasted image 20260318133918.png]]

Con la ip del objetivo seguido del puerto podemos ver lo que hay en ese puerto
![[Pasted image 20260318133947.png]]
Ejecutamos metasploit
![[Pasted image 20260318134007.png]]
Viendo la versión de openfire podemos buscar si existe ya algun exploit creado
![[Pasted image 20260318134018.png]]

Aqui podemos ver el exploit existente
![[Pasted image 20260318134127.png]]

![[Pasted image 20260318134138.png]]

Ponemos la ip del objetivo en RHOSTS
![[Pasted image 20260318134205.png]]
Ponemos nuestra ip en LHOST
![[Pasted image 20260318134359.png]]
Ejecutamos el exploit
![[Pasted image 20260318134410.png]]

Ya estamos dentro de la maquina objetivo
![[Pasted image 20260318134451.png]]

