Activamos ambas maquinas virtuales
![[Pasted image 20260221163951.png]]

Hacemos **ifconfig** para **obtener** nuestra **ip** en **eth0**
![[Pasted image 20260221164108.png]]

Si por lo que sea **ifconfig** **no funciona** de primeras tendriamos que **instalar las net-tools**
![[Pasted image 20260221164117.png]]

Con **sudo arp-scan -I eth0 --localnet** podemos **ver** las **ips disponibles** en nuestra **red local**, como pista las que empiezan en 08:00 son redes de virtualbox
![[Pasted image 20260221164228.png]]
Hacemos ping a la maquina objetivo, si ttl es 128,127 o similar es windows y si es similar a 64 suelen ser linux
![[Pasted image 20260221164551.png]]



