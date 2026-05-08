
| **IDENTIFICACIÓN**                                                                            | **AUTENTICACIÓN**                                                                                                             | **AUTORIZACIÓN**                                                                                               |
| --------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| Responde a la pregunta ¿Quién eres?                                                           | Responde a la pregunta ¿Eres quién dices ser?                                                                                 | Responde a la pregunta ¿Qué puedes hacer en el sistema?                                                        |
| Realizamos la identificación mediante un ID (normalmente nuestro correo o nombre de usuario). | Nos autenticamos en el sistema demostrando que somos quien decimos ser. Para esto, hacemos uso de contraseñas, biometría... . | El sistema verifica tus roles asociados y determina que acciones puedes ejecutar y que datos puedes consultar. |

**Identificación y autenticación:**
	Mecanismos: 
		Cuentas locales 
		LDAP | Active Directory 
		SAML | SSO 
	Configuración:
		Web UI 
		authentication.conf

**Autorización:**
	RBAC 
		Roles > Capabilities 
		Roles > Acceso a índices 
	Configuración: 
		Web UI 
		authorization.conf

**MODELO RBAC**
**Role Base Access Control (RBAC):** No se asignan permisos a las personas, se asignan personas a los roles.

![[Pasted image 20260412122022.png]]

### **Hardening y buenas prácticas**

**Auditoría interna:** 

Splunk registra automáticamente su propia actividad. Esto es crítico para cumplir normativas (GDPR, PCI, SOX) y para la resolución de problemas. 

**Índices clave**: 
- **index=_audit** : Contiene eventos de seguridad y auditoría. Registra quién ejecutó una búsqueda, quién modificó una configuración o quién se logueó. 
- **index=_internal** : Contiene logs sobre la salud del sistema (errores, advertencias, uso de licencia).  
 
 **Acción Recomendada**: Crear alertas automáticas que notifiquen si un usuario no autorizado intenta acceder a datos sensibles o si se borran objetos de conocimiento.


---

**Cifrado de comunicaciones:**

Por defecto, las instalaciones básicas pueden transmitir datos en texto plano. En un entorno de producción, toda la información en tránsito debe estar cifrada para evitar intercepciones (Man-in-the-Middle). 

**Puntos de aplicación:** 

• **Splunk Web (Puerto 8000):** Activar HTTPS para proteger las credenciales de inicio de sesión de los administradores y usuarios. 

• **Forwarding (Puerto 9997):** Configurar certificados SSL entre los Universal Forwarders y los Indexers para asegurar que los logs no sean leídos mientras viajan por la red.


---

**Autenticación: Tokens vs Contraseñas:**

El uso de usuarios y contraseñas en scripts o aplicaciones de terceros es una práctica de alto riesgo ("Hardcoded credentials"). 

**Solución (Tokens):** Splunk permite generar Tokens de Autenticación (Bearer Tokens). 

- **Ventajas**: Tienen fecha de caducidad, se pueden revocar sin cambiar la contraseña del usuario y permiten un control más granular. 
- **Uso**: Ideal para integración con APIs, scripts de Python o herramientas de orquestación (SOAR).

---

**Hardening del SO.**

El Hardening es el proceso de asegurar un sistema reduciendo su "superficie de ataque". Los sistemas operativos (Linux, Windows...) suelen venir configurados de fábrica priorizando la usabilidad y la compatibilidad sobre la seguridad, lo que implica puertos abiertos innecesarios, servicios superfluos y permisos laxos. 

El objetivo del hardening es cerrar esas brechas mediante acciones clave: 

- **Gestión de Vulnerabilidades**: Mantener el sistema y el kernel actualizados con los últimos parches de seguridad. 
- **Limpieza de Servicios**: Deshabilitar o desinstalar cualquier software, servicio o puerto de red que no sea indispensable para la función del servidor. 
- **Control de Red**: Configurar firewalls locales (ej. iptables, firewalld) para permitir tráfico únicamente en los puertos autorizados.


---

**Mínimos privilegios:**

Dicta que usuarios solo deben tener los accesos y permisos mínimos indispensables para realizar sus funciones específicas. Reduce drásticamente el riesgo de brechas de seguridad, errores accidentales y movimientos laterales al limitar la superficie de ataque y capacidad de daño. 
Se basa en el concepto de "necesidad de saber" (need-to-know). 

Aplica: 
- A los usuarios, roles y capacidades dentro del servicio de splunk. 
- Al propio usuario que ejecuta el servicio de Splunk desde el SO. 
	- Crear un usuario dedicado (ej. splunk). 
	- Asignar permisos de propietario solo al directorio /opt/splunk. 
	- Usar setfacl o sudo para permisos específicos si son necesarios.



