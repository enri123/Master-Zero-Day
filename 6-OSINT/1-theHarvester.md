**theHarvester** es una **herramienta OSINT** (Open Source Intelligence) de código abierto **escrita** en **Python**, diseñada para la recopilación pasiva de información durante la fase de reconocimiento en pruebas de penetración o evaluaciones de seguridad.

Ayuda a identificar el panorama de amenazas externas de un dominio objetivo recopilando correos electrónicos, subdominios, hosts, direcciones IP, nombres de empleados y puertos abiertos a partir de fuentes públicas.


Instalamos theHarvester, en sistemas enfocados a ciberseguridad se puede usar apt, en otros la instalación puede diferir.
![[Pasted image 20260216094651.png]]

Lista de comandos que se pueden usar con theHarvester
![[Pasted image 20260216100300.png]]

**Ejemplo de consulta**, usamos **-d** para **especificar** el **dominio** del que queremos que busque información, y **-b** para **especificar** la **fuente** de la cual va a sacar la información, en **-b** podemos poner **all**, para que busque en todas las fuentes disponibles. Para varias fuentes como por ejemplo **brave** y **bing** hace falta usar una **api**.
![[Pasted image 20260216100429.png]]

**Ejemplo de resultado** **buscando** el dominio **microsoft.com** en **yahoo**
![[Pasted image 20260216100546.png]]


