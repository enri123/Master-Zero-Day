Con **Nmap** podemos **obtener** los **puertos abiertos** de una **ip**
![[Pasted image 20260221165534.png]]

Estos son los puertos abiertos de esta maquina
![[Pasted image 20260221165605.png]]


![[Pasted image 20260221170056.png]]

El comando que aparece en la imagen es:

```bash
sudo nmap -sV -sC -sS -T5 -n -vvv -Pn 192.168.223.177 -oN Desktop/escaneo.txt
```

## 🔐 `sudo`

Ejecuta el comando con privilegios de superusuario.

Es necesario porque:

- El escaneo `-sS` (SYN scan) requiere acceso a sockets raw.
    
- Permite un escaneo más completo y preciso.
    

---

## 🔎 `nmap`

Es la herramienta de escaneo de red utilizada para:

- Descubrir hosts
    
- Detectar puertos abiertos
    
- Identificar servicios
    
- Fingerprinting del sistema operativo
    
- Ejecución de scripts NSE
    

---

## 🧩 `-sV` (Service Version Detection)

Activa la detección de versiones de los servicios.

Ejemplo:

- No solo detecta que el puerto 80 está abierto
    
- Sino que puede decir: `Apache httpd 2.4.52`
    

Esto ayuda en:

- Enumeración
    
- Identificación de vulnerabilidades específicas
    
- Matching con CVEs
    

---

## 📜 `-sC` (Default Scripts)

Ejecuta los **scripts por defecto del Nmap Scripting Engine (NSE)**.

Incluye scripts como:

- Enumeración básica
    
- Detección de vulnerabilidades comunes
    
- Información adicional sobre servicios
    

Es equivalente a:

```bash
--script=default
```

---

## ⚡ `-sS` (TCP SYN Scan – Stealth Scan)

También conocido como:

> Half-open scan

Funcionamiento:

1. Envía paquete SYN
    
2. Si recibe SYN-ACK → puerto abierto
    
3. Envía RST sin completar handshake
    

Ventajas:

- Más rápido que `-sT`
    
- Menos detectable (aunque no invisible)
    
- No completa la conexión
    

Muy usado en Red Team.

---

## 🚀 `-T5` (Timing Template 5 – Insane)

Controla la velocidad del escaneo.

Niveles:

- T0 → Muy lento
    
- T3 → Normal (default)
    
- T5 → Muy agresivo
    

⚠️ Riesgos:

- Puede generar falsos negativos
    
- Más fácil de detectar por IDS/IPS
    
- Puede causar DoS en sistemas frágiles
    

Se usa en entornos controlados o laboratorios.

---

## 🧠 `-n`

Desactiva la resolución DNS.

Evita:

- Consultas DNS reversas
    
- Retrasos innecesarios
    

Hace el escaneo:

- Más rápido
    
- Más discreto
    

---

## 🔊 `-vvv`

Nivel máximo de verbosidad.

Muestra:

- Más información en tiempo real
    
- Detalles de progreso
    
- Información de puertos conforme se descubren
    

Muy útil en pentesting manual.

---

## 🚫 `-Pn`

Significa:

> No Ping

Desactiva el host discovery.

Normalmente Nmap:

1. Hace ping primero
    
2. Si no responde → no escanea
    

Con `-Pn`:

- Asume que el host está activo
    
- Escanea directamente
    

Se usa cuando:

- El firewall bloquea ICMP
    
- Se quiere forzar el escaneo
    

En la imagen aparece el mensaje:

> Host discovery disabled (-Pn). All addresses will be marked 'up'

---

## 🎯 `192.168.223.177`

Es el objetivo del escaneo.

Pertenece a un rango:

- `192.168.x.x` → red privada (RFC1918)
    

---

## 💾 `-oN Desktop/escaneo.txt`

Guarda el resultado en formato normal (legible) en:

```
Desktop/escaneo.txt
```

Tipos de salida comunes:

- `-oN` → normal
    
- `-oX` → XML
    
- `-oG` → grepable
    
- `-oA` → todos los formatos
    

Muy importante en:

- Reportes
    
- Evidencia forense
    
- Automatización
    
