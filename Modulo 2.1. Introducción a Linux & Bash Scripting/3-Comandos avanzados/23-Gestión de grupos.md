Usando **ls -l** podemos ver el creador, el primer nombre, y el grupo, el segundo grupo.
Usando **sudo addgroup** podemos crear un nuevo grupo
![[Pasted image 20260301113052.png]]

Añadimos el nuevo usuario gustavo usando adduser
![[Pasted image 20260301113150.png]]

Añadimos el grupo profesores a pepe y gustavo, usando usermod -ag.
Usando getent group profesores, podemos ver los usuarios que pertenecen a ese grupo
![[Pasted image 20260301113323.png]]

Usando chown podemos señalar que queremos que un archivo pertenezca a cierto grupo, en este caso profesores
![[Pasted image 20260301113422.png]]

Eliminamos el grupo profesores usando groupdel
![[Pasted image 20260301114001.png]]