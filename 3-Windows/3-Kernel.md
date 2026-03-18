**El corazón de Windows**
- Ubicación: **C:\Windows\System32\ntoskrnl.exe**
- NT viene de "New Technology" - arquitectura que microsoft introdujo con Windows NT 3.1 en 1993.
- Es el archivo ejecutable más crítico el sisema. Sin él, Winndows no arranca.

**Las 4 responsabilidades principales del kernel**
- **Gestión de Procesos y Threads**
	1. Scheduler: Decide qué proceso usa el CPU e cada momento
	2. Windows usa scheduling  preventivo con prioridades (0-31)
	3. Puede interrumpir un proceso para dar CPU a otro más prioritario
	4. Cada proceso tiene al menos 1 thread (hilo de ejecución)

- **Gestión de Memoria**
	1. Implementa memoria virtual: permite ejecutar más programas que RAM física disponible
	2. Paginación: divide  memoria en páginas de 4KB
	3. Cuando RAM se llena, mueve páginas al disco (pagefile.sys)
	4. Esto es por qué un PC con 8GB RAM puede ejecutar programas que suman 12GB

- **Gestión de I/O**
	1. Todo acceso a disco, red, USB, impresora pasa por el kernel
	2. Proporciona abstracción: las apps no necesitan saber cómo funciona cada dispositivo
	3. El kernel coordina con los drivers para hablar con el hardware

- **Seguridad**
	1. Enforces el modelo de seguridad de Windows
	2. Verifica permisos en cada acceso a recursos (archivos, registro, objetos)
	3. Security Reference Monitor: componente del kernel que valida access tokens contra ACLs
	4. Ejemplo: Cuando intentas abrir un archivo, el kernel verifica si tu token tiene los permisos necesarios según el ACL del archivo

- **HAL.dll - Hardware Abstraction Layer**
	1. Se carga siempre junto al kernel
	2. Proporciona interfaz común para hardware diferente
	3. Permite que el mimo kernel funcione en PCs con diferentes configuraciones de hardware 

- **Ring 0 vs Ring 3**
	1. Arquitectura de protección de procesadores x86
	2. Ring 0 (Kernel Mode): Acceso completo a hardware, puede ejecutar cualquier instrucción
	3. Ring 3 (User Mode): Acceso restringido, no puede tocar hardware directamente
	4. **Analogía**: Ring 0 es como tener llaves maestras del edificio, Ring 3 es como ser un inquilino que necesita pedir permiso al conserje
