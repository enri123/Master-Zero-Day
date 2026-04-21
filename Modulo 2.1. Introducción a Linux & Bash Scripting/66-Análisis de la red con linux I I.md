![[Pasted image 20260309221828.png]]

**`arp-scan -I enp0s3 --localnet | grep -v "Interface" |  grep -v "Starting" | grep -v "Starting" | grep -v "Starting" | awk '{print $1}' | tr -d ' ' > ips.txt`**

Con **arp-scan** podemos **ver** todas las **direcciones Ip disponibles en nuestra red local**, y con **grep** vamos quitando todas las lineas de texto que no nos interesan, y por ultimo usamos **awk**, para cojer solo la primera columna de las lineas de las ip, que son las que nos interesan, y hacemos un **tr**, por si se queda algún espacio suelto, el resultado lo enviamos a una fichero llamado **ips.txt**, para su posterior lectura
![[Pasted image 20260309221918.png]]

Hacemos un **while** con todas las **ip** almacenadas en el **.txt** que nos ha dado el **arp-scan**, y de cada una de estas **ips** les hacemos un **nmap**

**`nmap  -p- -sS -sV --min-rate=5000 -n -Pn $linea -oN "escaneo_$linea"`**
![[Pasted image 20260309223838.png]]


![[Pasted image 20260309223913.png]]


