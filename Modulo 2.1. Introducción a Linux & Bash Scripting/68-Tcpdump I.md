Usamos ifconfig para ver la ip de la maquina y el tipo de red, en este caso eth0
![[Pasted image 20260311143606.png]]

Usamos tcdump para analizar el trafico de la red, y usamos -i eth0, para ver especificamente el trafico  de la interfaz de red eth0
![[Pasted image 20260311143622.png]]

Filtramos el analisis a solo icmp, los icmp son los request, destino inalcanzable, tiempo excedido, redireccionamiento
![[Pasted image 20260311143737.png]]

Hacemos que el resultado me lo escriba en **trafico.pcap**
![[Pasted image 20260311143823.png]]

**Wireshark** es una herramienta que nos permite analizar los datos de manera mas facil
![[Pasted image 20260311143939.png]]

![[Pasted image 20260311144002.png]]

Aqui podemos ver la contraseña y el usuario, usuario pinguino y contraseña elbubu
![[Pasted image 20260311144035.png]]

