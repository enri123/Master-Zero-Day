
**Qué son los servicios?**
- Programas que se ejecutan en segundo plano sin interfaz de usuario
- Equivalente a "daemons" en Linux/Unix
- Pueden arrancar antes de que cualquier usuario haga login
- Proporcionan funcionalidades fundamentales del sistema

**Service Control Manager (SCM)**
- Proceso: services.exe
- Es el "jefe" de todos los servicios
- Arranca muy temprano en el boot (fase 5 del proceso de arranque)
- Responsable de iniciar servicios automáticos, gestionar dependencias
- Sí services.exe falla -> Blue Screen (es crítico)

**Ubicación de configuración**
- Registro: **HKLM\SYSTEM\CurrentControlSet\Services\**
- Cada servicio tiene su subclave aquí
- Contiene: tipo de inicio, cuenta de servicio, dependencias, ruta del ejecutable

**Tipos de Inicio**
- **Automatic**
	- Inicia automáticamente al arrancar Windows
- **Automatic (Delayed Start)**
	- Inicia automáticamente PERO 2 minutos después del arranque
- **Manual**
	- No inicia automáticamente
	- Puede ser iniciado por: otro servicio que dependa de él, un programa, o manualmente por admin
- **Disabled**
	- Completamente deshabilitado
	- No puede iniciarse ni manual ni automáticamente


Los servicios no ejecutan "en el vacío", necesitan una identidad (cuenta de usuario) para ejecutar la identidad determina qué permisos tienen.
- **LocalSystem (NT AUTHORITY\SYSTEM)**
	- La cuenta más poderosa del sistema

- **LocalService (NT AUTHORITY\LOCAL SERVICE)**
	- Privilegios reducidos, similares a un usuario del grupo "Users"

- **NetworkService (NT AUTHORITY\NETWORK SERVICE)**
	- Similar a LocalServices en privilegios locales
	- PERO tiene credenciales de red usando la identidad de la computadora

- **Cuentas Personalizadas**
	- Puedes configurar un servicio para ejecutarse con cualquier cuenta

Servicios Críticos que deberías conocer:

- **wuauserv - Windows Update**:Descarga e instala actualizaciones
- **Spooler - Print Spooler**:Gestiona cola de impresión (explotado históricamente)
- **BITS - Background Inelligent Transfer Service:** Usado por Windows Update para descargas en segundo plano
- **Dnscache - DNS Client**: Cache respuestas DNS para acelerar resoución
- **Dhcp - DHCP Client**: Obtiene configuración de red automáticamente
- **LanmanServe - Server**: Proporciona compartición de archivos SMB/CIFS
- **LanmanWorkstation - Workstation**: Cliente SMB, permite acceder a recursos compartidos
- **EventLog -Windows Event Log**: Sistema de logging, si falla no hay logs
- **RpcSs - Remote Procedure Call**: Base para comunicación entre procesos, crítico
