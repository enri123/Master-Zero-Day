Decargamos la maquina Canto
![[Pasted image 20260329164408.png]]

Con arp-scan escaneamos las ips disponibles en nuestra maquina local, y sabemos que la maquina virtual es la primera, por que empieza en 08:00
![[Pasted image 20260329164625.png]]

Con nmap hacemos un scaneo de puertos en la maquina objetivo, y lo guardamos en el archivo escaneo, para que haga menos ruido
![[Pasted image 20260329164713.png]]

Buscamos la url en el buscador, y llegamos a la maquina objetivo
![[Pasted image 20260329164740.png]]

Nos metemos en el codigo fuente de la página y comprobamos que es un wordpress y la versión de wordpress
![[Pasted image 20260329164804.png]]


Con wpscan y la url objetivo, le decimos -e u,p, para que nos intente encontrar los usuarios y los plugins de esta página de wordpress
![[Pasted image 20260329164847.png]]

wpscan, no encuentra plugins, pero si un usuario
![[Pasted image 20260329164931.png]]

Podemos introducir a wpscan una api-token, para que realice una búsqueda mas exahustiva
![[Pasted image 20260329164945.png]]

Podemos encontrar el token iniciando sesión en la página web de wpscan
![[Pasted image 20260329165000.png]]

![[Pasted image 20260329165013.png]]
![[Pasted image 20260329165019.png]]
En este caso, no hay diferencia
![[Pasted image 20260329165036.png]]

Podemos pedirle a wpscan que realice una detección de plugins agresiva, esto es mucho mas ruidoso
![[Pasted image 20260329165042.png]]

En este caso, si que nos encuentra el plugin objetivo
![[Pasted image 20260329165113.png]]

Buscamos en google el exploit, para atacar la vulnerabilidad
![[Pasted image 20260329165133.png]]

Otra forma de buscar plugins es con una wordlist
![[Pasted image 20260329165256.png]]

![[Pasted image 20260329165307.png]]

Obtenemos la wordlist
![[Pasted image 20260329165321.png]]

Realizamos un dir, usando la wordlist, la url wp-content/plugins/ es la url típica donde se encuentran los plugins de wordpress
![[Pasted image 20260329165347.png]]-
En este caso el dir nos encuentra dos plugins
![[Pasted image 20260329165405.png]]

