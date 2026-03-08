Importatne tener ambas maquinas virtuales activadas
![[Pasted image 20260305210157.png]]

Para poder crear un servidor ftp necesitamos instalar vsftpd
![[Pasted image 20260305210403.png]]


Usando status podemos comprobar si el servidor esta activo, en caso de que no lo este podemos ejecutar start en lugar de status para iniciarlo
![[Pasted image 20260305210434.png]]

Usando ftp y la ip de la maquina servidor podemos conectarnos desde cualquier otra maquina
![[Pasted image 20260305210639.png]]

Descomentamos write_enable, para poder ejecutar comandos
![[Pasted image 20260305210934.png]]

Importante reiniciar despues de esto
![[Pasted image 20260305211021.png]]

Nos volvemos a conectar desde cliente
![[Pasted image 20260305211056.png]]

![[Pasted image 20260305211109.png]]

