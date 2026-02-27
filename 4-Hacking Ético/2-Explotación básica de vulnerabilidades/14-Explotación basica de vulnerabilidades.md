Usaremos la herramienta **metasploit**, que nos ayudará a **automatizar explotaciones** ya conocidas
![[Pasted image 20260223131638.png]]

Con **search** nos **mostrará los distintos exploits** que existen para una determinada vulnerabilidad
![[Pasted image 20260223131655.png]]

**Usamos** uno de los **exploits** que nos ha **mostrado** con **search**
![[Pasted image 20260223132604.png]]

Una ves seleccionamos un **exploit** usando **show options** nos mostraran distintos datos, algunos como el host tendremos que introducirlos nosotros mismos, en este caso el puerto esta puesto **automaticamente**, pero puede ser que nos lo pidan
![[Pasted image 20260223132710.png]]

En este caso usaremos el host de nuestra maquina virtual objetivo
![[Pasted image 20260223132813.png]]

Como podemos ver aqui ya aparece puesta en **options**
![[Pasted image 20260223132823.png]]

Ejecutamos run, para que comience el exploit
![[Pasted image 20260223132929.png]]

Como podemos ver ha sido **exitosa**, por lo que estamos dentro del **meterpreter**
![[Pasted image 20260223132951.png]]

El **meterpreter** no nos permite ciertas funciones, por lo que en este caso **ejecutamos shell**, para poder navegar dentro de la maquina objetivo
![[Pasted image 20260223133034.png]]

