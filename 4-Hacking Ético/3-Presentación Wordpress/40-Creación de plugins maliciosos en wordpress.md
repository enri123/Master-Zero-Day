Nos instalamos la maquina de dockerlabs de BadPlugin
![[Pasted image 20260329172039.png]]

Iniciamos la maquina
![[Pasted image 20260329172103.png]]
Como podemos ver de primeras la ip proporcionada por la maquina no nos vale
![[Pasted image 20260329172142.png]]

Simplemente en etc/hosts tenemos que poner la ip proporcionada con el dominio que nos aparece la buscar la ip
![[Pasted image 20260329172206.png]]

Ya nos funciona
![[Pasted image 20260329172226.png]]

Buscamos acceder a la url de inicio de sesión de wordpress, en este caso el usuario y la contraseña son las mismas que en apartado 36
![[Pasted image 20260329172242.png]]

Accedemos al panel de administrador de wordpress, y vamos a la sección de plugins
![[Pasted image 20260329172256.png]]

Si intentamos subir un plugin desde el servidor no nos lo va a permitir, por lo que lo vamos a instalar desde local
![[Pasted image 20260329172311.png]]

Realizamos el plugin malicioso
![[Pasted image 20260329172344.png]]

Lo convertimos en un .zip
![[Pasted image 20260329172408.png]]

Lo instalamos en el servidor desde local
![[Pasted image 20260329172422.png]]
Activamos el plugin malicioso
![[Pasted image 20260329172427.png]]
Escuchamos el puerto seleccionado en el plugin
![[Pasted image 20260329172438.png]]

