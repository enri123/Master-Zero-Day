https://labs.thehackerslabs.com/machine/181
![[Pasted image 20260522190412.png]]

Accedemos a la pagina vulnerable
![[Pasted image 20260522190514.png]]

La parte que nos interesa en este caso es la pagina de login
![[Pasted image 20260522190524.png]]

Activamos burpsuit para obtener el envio del login
![[Pasted image 20260522190549.png]]

Buscamos un payload para un injección sql
https://swisskyrepo.github.io/PayloadsAllTheThings/NoSQL%20Injection/
![[Pasted image 20260522190600.png]]

Enviamos el proxy al repeater, y sustituimos el usuario y la contraseña por el payload
![[Pasted image 20260522190640.png]]

Acceso concedido
![[Pasted image 20260522190655.png]]

http://labs.thehackerslabs.com/machines/share/z3sLWJiFPl9IbMh7iUaqg317-dfUGLDK8ZxLb1yQlKY
![[Pasted image 20260522191149.png]]