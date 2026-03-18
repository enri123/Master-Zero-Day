**Qué es un sistema operativo?**
Un sistema operativo es el software que actúa como intermediario entre el hardware de nuestro ordenado y las aplicaciones que ejecutamos.

**Capas**: Hardware + HAL + Kernel + Servicios + Aplicaciones
**HAL**: Hardware Abstraction Layer - portabilidad
**Kernel** (ntoskrnl.exe): Núcleo de SO
1. **Gestiona**: mmoria, procesos, I/O, seguridad.
2. **Modo Kernel** (Ring 0) vs **Modo Usuario** (Ring 3)
**Modo Kernel** -> **Admin**
**Modo Usuario** -> **User**

**Proceso de Arranque**
1. **POST**: Power-On Self-Test por BIOS/UEFI
2. **BIOS/UEFI** carga bootloader (MBR o GPT)
3. **Windows Boot Manager** lee BCD
4. **Windows Loader** carga kernel (ntoskrnl.exe)
5. **Kernel** inicializa drivers y servicios
6. **Winlogon.exe** presenta pantalla de login

**Fase 1: Post - Power-on Self-Test**

Al encender el ordenador lo primero que se ejecuta es el firmware del ordenador, que puede ser BIOS o UEFI.

Este firmware hace un POST, una autoverificación del hardware: verifica que hay RAM, que el procesador funciona, que hay un disco de arranque disponible.

**Fase 2: BIOS/UEFI carga bootloader**

El firmware busca en el disco un bootloader.
	En sistemas con BIOS, busca en el MBR (Master Boot Record) que está en el primer sector del disco
	En sistemas UEFI, busca en la EFI System Partition, una partición especial formateada en FAT32

Una vez localizado el bootloader, lo carga en memoria y le pasa el control.

**Fase 3: Windows Boot Manager**

El bootloader de Windows se llama Windows Boot Manager, o bootmgr

Este programa lee un archivo de configuración llamado BCD (Boot Configuration Data) que contiene información sobre que sistemas operativos están instalados y cómo arrancarlos.

Si tenemos un dual boot, por ejemplo Windows y Linux, aquí es donde veis el menú para elegir que sistema arrancar.

**Fase 4: Windows Loader carga kernel** 

Una vez seleccionado Windows, el Boot Manager carga el Windows Loader (winload.exe).
Este programa finalmente carga en memoria el kernel de Windows, ntoskrnl.exe, y también carga el HAL, hal.dll.

**Fase 5: Kernel inicializa drivers y servicios**

Con el kernel en memoria, éste comienza a inicializar los subsistemas.

Carga los driver críticos que necesita para acceder al disco y otros dispositivos.

Luego inicia el Session Manager el proceso que se encarga de crear las sesiones de usuario.

**Fase 6: Winlogon.exe presenta pantalla de login**

Finalmente, se inicia **winlogon.exe**, que presenta la pantalla de inicio de sesión.

Y aquí es cuando vosotros introducís vuestra contraseña y empezáis a usar el sistema.

**BIOS vs UEFI**

**BIOS**
	Firmware clásico (1975), arquitectura 16 bits.
	Solo funciona con MBR
	Limite de 2TB por disco
	Máx 4 participaciones primarias.

**UEFI**
	Firmware actual (desde 2005), 32/64 bits
	Usa GPT
		Soporta discos de hasta 9,4ZB
		Hasta 128 participaciones
	Secure Boot
		Verifica la firma digital del bootloader
		Bloque bootkits/rootkits
		Arranque de Windows firmado por Microsoft; Linux requiere configuración adicional.
	

**Windows Boot Manager (bootmgr)**

El **bootmgr** es un pequeño programa que reside en la raíz del disco de sistema. Su trabajo es leer la configuración de arraque  y presentar el menú si hay multiples sistemas operativos.

	En sistemas BIOS está em C:/bootmgr
	En sustemas UEFI está en la EFI System Partition, en EFI\Microsoft\Boo\bootmgfw.efi

**BCD - Boot Configuration Data**

El archivo **BCD** es como el antiguo boot.ini de Windows XP, pero muchísimo más complejo. Es prácticamente una base de datos que contiene toda la configuración de arranque.

	El BCD se encuentra en C:\Boot\BCD en sistemas BIOS.
	En EFI\Microsoft\Boot\BCD en sistemas UEFI.

**Herramienta bcdedit**

Para manipular el BCD, Windows proporciona **bcdedit.exe**. Requiere privilegios de administrados.


