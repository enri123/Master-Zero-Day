Usaremos la herramienta msfvenom para crear un viruz
![[Pasted image 20260318135001.png]]

En LHOST pondremos nuestra IP, y en LPORT el puerto desde el que escucharemos, -o es el nombre que le pondremos al viruz
![[Pasted image 20260318152358.png]]

Creamos el viruz y encendemos un servidor, para descargarnos el viruz desde la maquina objetivo
![[Pasted image 20260318152727.png]]

Nos descargamos el viruz
![[Pasted image 20260318152605.png]]

Encendemos metasploit en la maquina atacante
![[Pasted image 20260318152752.png]]


![[Pasted image 20260318152812.png]]

Indispensable que el payload, LHOST Y LPORT coincidan con los datos introducidos anteriormente
![[Pasted image 20260318152851.png]]
![[Pasted image 20260318152927.png]]
Ejecutamos el exploit, y cuando el objetivo ejecute el .exe, tendremos conexión con su maquina
![[Pasted image 20260318153058.png]]


