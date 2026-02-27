Si ejecutamos **firefox** tal cual se nos va a abrir en **linux**, pero nos va a ocupar la teminal en primer plano
![[Pasted image 20260225180723.png]]

Si le **añadimos una &**, se ejecutara en segundo plano y podremos seguir usando la terminal
![[Pasted image 20260225180829.png]]

Si ejecutamos **jobs**, podremos ver los procesos abiertos y su estado
![[Pasted image 20260225180903.png]]

con **fg** pasamos el proceso a primer plano y vueve a ocupar la terminal
![[Pasted image 20260225180936.png]]

Con **control z** podemos suspender el proceso en primer plano
![[Pasted image 20260225180948.png]]

![[Pasted image 20260225181008.png]]

Con **bg** pasamos el proceso en segundo plano y ademas se activa
![[Pasted image 20260225181022.png]]

Con **fg %1** ponemos el proceso al que equivalga 1 que en este caso es firefox en promer plano
![[Pasted image 20260225181105.png]]

Con **pgrep** podemos ver el numero al que equivale el proceso, y con **kill** mas ese numero lo eliminamos
![[Pasted image 20260225181223.png]]

Con **ps aux** podemops ver todos los procesos de linux
![[Pasted image 20260225181259.png]]

![[Pasted image 20260225181321.png]]