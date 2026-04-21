Controladores Aka Drivers
**Qué son los drivers?**
- Software que permite al sistema operativo comunicarse con los dispositivos del hardware
- Actúan como "traductores" entre el kernel y el hardware
- Sin driver apropiado, el hardware es inútil para el SO
- Ubicación de drivers: Kernel-mode: **C:\Windows\System32\drivers\**

**Tipos de Drivers:**
- **Kernel-mode drivers (.sys)**
	- Ejecutan en Ring 0 (modo kernel)
	- Acceso directo y sin restricciones al hardware
	- Pueden acceder a toda la memoria del sistema
	- Riesgo: Un driver mal programado puede causar Blue Screen
	- Ejemplo: Driver de tarjeta gráfica NVIDIA (nvlddmkm.sys), driver de red Intel (e1d68x64.sys)

- **User-mode drivers**
	- Ejecutan en Ring 3 (modo usuario)
	- Acceso limitado, más seguros
	- Si fallan, no causan Blue Screen
	- Menos comunes, usados para dispositivos, menos críticos
	- Ejemplo: Drivers de impresoras modernas, algunos drivers de cámara web


**El registro de windows**

**Qué es el Registro?**
- Base de datos jerárquica centralizada
- Almacena configuración de bajo nivel del SO y aplicaciones
- Introducido en Windows 3.1 (1992) para reemplazar archivos .INNI dispersos
- 
![[Pasted image 20260313070234.png]]

![[Pasted image 20260313070247.png]]

![[Pasted image 20260313070304.png]]

![[Pasted image 20260313070324.png]]

