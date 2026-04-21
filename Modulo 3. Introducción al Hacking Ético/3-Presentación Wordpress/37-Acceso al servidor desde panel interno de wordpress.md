Usando el usuario y contraseña, podemos acceder al panel de administrador de wordpress
![[Pasted image 20260329151312.png]]

Si la maquina objetivo tiene instalado algún editor de codigo podemos modificarlo para introducir un malware
![[Pasted image 20260329151328.png]]

En la sección de plugins podemos ver los plugins instalados y en el caso de que se pueda instalar nuevos plugins
![[Pasted image 20260329151344.png]]

En el editor de codigo borramos el index.php
![[Pasted image 20260329151517.png]]

Descargamos de github el malware
![[Pasted image 20260329151524.png]]

Copiamos el .php
![[Pasted image 20260329151535.png]]

Cambiamos la ip y el puerto, para poner el nuestro
![[Pasted image 20260329151557.png]]

Empezamos a escuchar el puerto que hayamos seleccionado
![[Pasted image 20260329161332.png]]

Miramos la url donde se encuentra el archivo modificado
![[Pasted image 20260329161402.png]]

Hacemos un dirb
![[Pasted image 20260329161444.png]]

Miramos los distintos directorios disponibles
![[Pasted image 20260329161453.png]]

En el navegador buscamos la url objetivo
![[Pasted image 20260329161520.png]]

Ya tendriamos acceso a la maquina objetivo
![[Pasted image 20260329161547.png]]

