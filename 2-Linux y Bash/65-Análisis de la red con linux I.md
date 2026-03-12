
**`hostname -I`** → Muestra **las direcciones IP locales** asignadas al host (solo IPs, sin información adicional).
![[Pasted image 20260307213846.png|324]]

**`ip a`** → Comando moderno de Linux para **listar todas las interfaces de red**, sus IPs, MAC, estado (UP/DOWN) y configuración.
![[Pasted image 20260307214414.png]]

**`ifconfig`** → Herramienta clásica (obsoleta en muchas distros) para **ver y configurar interfaces de red** e IPs del sistema.
![[Pasted image 20260307214502.png]]

**`sudo arp-scan -I enp0s3 --localnet`** → Escanea la **red local mediante ARP** para descubrir **dispositivos activos y sus MAC/IP** en la interfaz `enp0s3`.
![[Pasted image 20260307214722.png]]

**`nmap 192.168.0.17`** → Escaneo básico de Nmap que **detecta puertos abiertos comunes** en el host objetivo.
![[Pasted image 20260307214902.png]]

**`nmap -p- 192.168.0.17`** → Escanea **todos los 65,535 puertos TCP** del host para encontrar cualquier servicio abierto. 🔎
![[Pasted image 20260307214929.png]]



