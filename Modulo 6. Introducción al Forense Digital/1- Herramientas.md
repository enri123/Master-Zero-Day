
---

# 🧪 Herramientas de Forense Digital (DFIR)

## 🔎 FTK Imager

**Descarga**: https://www.exterro.com/digital-forensics-software/ftk-imager

**Tipo:** Adquisición forense

**Descripción:**  
Herramienta para crear imágenes forenses de discos y visualizar contenido sin alterar la evidencia.

**Funciones:**

- Creación de imágenes (E01, RAW)
    
- Hashing (MD5, SHA)
    
- Preview de discos
    

**Ventajas:**

- Fácil de usar
    
- Portable
    
- Mantiene integridad de evidencia
    

**Limitación:**

- Análisis limitado
    

---

## 🔎 WinHex

**Descarga**: https://x-ways.net/winhex/

**Tipo:** Análisis low-level / Hexadecimal

**Descripción:**  
Editor hexadecimal avanzado para análisis profundo de datos.

**Funciones:**

- Análisis binario
    
- Recuperación de datos
    
- Disk carving manual
    

**Ventajas:**

- Control total a bajo nivel
    
- Muy potente en análisis manual
    

**Limitación:**

- Curva de aprendizaje alta
    

---

## 🔎 Disk2vhd
![[Pasted image 20260424110653.png]]

**Tipo:** Conversión / Virtualización

**Descripción:**  
Es el administrador de equipos de windows, pero antes de windows 10 se llamaba Disk2vhd.
Convierte discos físicos en máquinas virtuales (VHD/VHDX).

**Funciones:**

- Clonado a entorno virtual
    
- Migración de sistemas
    

**Ventajas:**

- Permite análisis seguro
    
- No requiere hardware original
    

**Uso típico:**

- Análisis de sistemas comprometidos
    

---

## 🔎 Guymager

**Descarga**: sudo apt install guymager

**Tipo:** Adquisición forense (Linux)

**Descripción:**  
Herramienta open source para adquisición de discos.

**Funciones:**

- Imagen forense
    
- Hash automático
    

**Ventajas:**

- Muy rápida
    
- Open source
    
- Estable y confiable
    

---

## 🔎 OSFMount

**Descarga**: https://www.osforensics.com/tools/mount-disk-images.html

**Tipo:** Montaje de imágenes

**Descripción:**  
Permite montar imágenes como discos en Windows.

**Funciones:**

- Montaje read-only
    
- Soporte múltiples formatos
    

**Ventajas:**

- Ligera
    
- Rápida
    
- Ideal para análisis rápido
    

---

## 🔎 Arsenal Image Mounter

**Descarga**: https://arsenalrecon.com/downloads

**Tipo:** Montaje avanzado

**Descripción:**  
Herramienta profesional para montar imágenes forenses.

**Funciones:**

- Emulación completa de discos
    
- Montaje forense real
    

**Ventajas:**

- Alta fidelidad
    
- Compatible con herramientas DFIR
    

---

## 🔎 EWF Tools

**Tipo:** Manipulación de formato E01

**Descripción:**  
Suite para trabajar con imágenes forenses EWF.

**Funciones:**

- Conversión
    
- Extracción
    
- Gestión de evidencias
    

**Ventajas:**

- Open source
    
- Estándar en forense
    

---

## 🔎 Autopsy

**Descarga**: 
Windows
https://www.autopsy.com/download/
Linux
Sudo apt install autopsy

**Tipo:** Análisis forense (GUI)

**Descripción:**  
Plataforma completa de análisis digital.

**Funciones:**

- Timeline
    
- Análisis de artefactos
    
- Navegación web
    

**Ventajas:**

- Interfaz amigable
    
- Automatización
    
- Basado en Sleuth Kit
    

---

## 🔎 Volatility

**Descarga**: 

sudo apt update
sudo apt install python3-venv python3-pip git -y   
mkdir ~/tools && cd ~/tools
python3 -m venv vol3_env
source vol3_env/bin/activate   
pip install volatility3
 vol -h   


**Tipo:** Análisis de memoria RAM

**Descripción:**  
Framework para análisis de memoria en vivo.

**Funciones:**

- Procesos activos
    
- Conexiones de red
    
- Malware fileless
    

**Ventajas:**

- Detecta amenazas avanzadas
    
- Clave en incident response
    

---

# 🧩 Flujo DFIR

```mermaid
flowchart LR
A[Adquisición] --> B[Montaje]
B --> C[Análisis Disco]
C --> D[Análisis Memoria]
```

**Herramientas por fase:**

- **Adquisición:** FTK Imager, Guymager
    
- **Montaje:** OSFMount, Arsenal Image Mounter
    
- **Conversión:** Disk2vhd, EWF Tools
    
- **Análisis Disco:** Autopsy, WinHex
    
- **Memoria:** Volatility
    

