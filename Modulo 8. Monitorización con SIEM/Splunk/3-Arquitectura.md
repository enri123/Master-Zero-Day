Splunk sigue una arquitectura modular y distribuida. Se compone de varios roles que cooperan:
	Recolección → Forwarders 
	Indexación → Indexers 
	Búsqueda y visualización → Search Heads 
	Gestión y soporte → Deployment Server, Cluster Master,License Manager…

**Objetivo de la arquitectura:** 
	Ingestar datos en tiempo real. 
	Indexarlos eficientemente. 
	Permitir búsquedas rápidas y escalables. 
	Soportar alta disponibilidad (HA) y redundancia.

![[Pasted image 20260412115438.png]]


### **Single instance**

**Componentes en un solo servidor** 
	Forwarder (opcional, si se envían logs externos) 
	Indexer 
	Search Head

**Ventajas** 
	Simple 
	Fácil de instalar 
	Ideal para demos y aprendizaje

**Limitaciones**
	No escalable 
	Sin redundancia 
	Cuello de botella en CPU, I/O y almacenamiento

**¿Cuándo se usa?** 
	Laboratorios 
	Entornos de desarrollo 
	Pymes con pocos datos

### **Componentes 1: forwarder**

**Función principal** 
	• Recolectar logs de servidores, firewalls, aplicaciones, cloud, etc. 
	• Enviar los datos a los indexers de Splunk usando protocolo propietario seguro.

**Tipos de forwarders:**

1. Universal Forwarder (UF) 
	• El más común. 
	• Ligero, silencioso, ideal para servidores y endpoints. 
	• Solo envía datos (no indexa ni interpreta). 
	• Consume pocos recursos (<2% CPU normalmente).
2. Heavy Forwarder (HF) 
	• Versión completa de Splunk como forwarder. 
	• Puede parsear, filtrar y enrutar datos antes de enviarlos. 
	• Recomendado para: 
		• Splunk Cloud 
		• Filtrado previo de eventos 
		• Normalización avanzada

**Notas** 
	• Se configuran mediante inputs.conf. 
	• Los Heavy Forwarders además usan props.conf y transforms.conf.

### **Componentes 2: indexers**

**¿Qué hace un indexer?** 
	• Recibe los datos desde forwarders u otras fuentes. 
	• Parseo y normalización de los eventos. 
	• Indexación y almacenamiento. 
	• Gestiona la retención y el ciclo de vida de los datos. 
	• Devuelve resultados de búsqueda cuando se le consulta.

Splunk almacena los datos en "buckets": 
	• **Hot** (actual, escritura activa) 
	• **Warm** (recientes) 
	• **Cold** (poco frecuentes) 
	• **Frozen** (archivados o eliminados)

**Factor crítico** 
Los indexers deben tener almacenamiento rápido (SSD), alto throughput y buena red.

### **Componentes 3: Search head**

**Funciones** 
	• Recibe las consultas SPL del usuario. 
	• Divide la búsqueda en partes y las envía a los indexers. 
	• Recopila los resultados y genera: 
	• Dashboards 
	• Visualizaciones 
	• Alertas 
	• Reportes

**Tareas típicas** 
	• Guardar búsquedas programadas. 
	• Gestión de Knowledge Objects: 
	• Field Extractions 
	• Lookups 
	• Macros 
	• Event Types 
	• Data Models

**Importante** 
Los search heads no almacenan datos.

### **INDEXER CLUSTERING**

**Objetivo**
	• Alta disponibilidad 

**Componentes** 
	• **Cluster Master / Manager**: coordina el cluster 
	• **Indexers (Peers):** almacenan y replican datos 
	• **Replication Factor**: cuántas copias de cada dato 
	• **Search Factor**: cuántas copias listas para consulta

**¿Por qué es esencial?** 
	• Los datos se replican entre varios indexers. 
	• Si un indexer cae, no se pierde información ni capacidad de procesado

### **SEARCH HEAD CLUSTERING**

**Objetivos** 
	• Alta disponibilidad 
	• Balanceo de carga 
	• Sincronización del conocimiento (KO)

**Componentes** 
	**• Search Heads Members** 
	• **Captain**: coordina búsquedas, programaciones, etc. 
	• **Deployer**: Coordina los Search Heads.

**Problema que resuelve** 
Evitar perder dashboards, alertas o modelos de datos si un search head falla.

### **MULTISITE**

**¿Qué es?** 
**Distribución del** Indexer Cluster y Search Head Cluster en varios centros de datos (sites) para lograr **alta disponibilidad geográfica y recuperación ante desastres (DR)**

**Cómo funciona** 
	• Los indexers se organizan por sites. 
	• Splunk replica datos entre sites según: 
		▪ **Replication Factor (RF)** multisite 
		▪ **Search Factor (SF)** multisite 
	• Si un site falla, otro **mantiene los datos y las búsquedas operativas**.

**Ventajas** 
	• Tolerancia a caída total de un site 
	• Optimización de búsquedas locales 
	• Escalabilidad horizontal y mejor resiliencia

**Casos de uso** 
	• Requerimientos estrictos de continuidad y DR 
	• Organizaciones distribuidas geográficamente 
	• Regulación y data residency

### **Componentes adicionales**

**Deployment Server** 
	• Centraliza la distribución de configuraciones a múltiples forwarders o instancias. 
	• Útil para entornos con miles de máquinas.

**License Manager** 
	• Gestiona las licencias y el consumo diario. 
	• Permite controles granulares por pool o proyecto.

**Monitoring Console** 
	• Herramienta interna de Splunk para: 
		▪ Monitorizar rendimiento 
		▪ Analizar indexación 
		▪ Revisar problemas de infraestructura

### **SPLUNK CLOUD**

**¿Qué simplifica?** 
	• Back-end gestionado por Splunk 
	• Alta disponibilidad garantizada 
	• Actualizaciones automáticas

**¿Qué sigue dependiendo del cliente?** 
	• Envío de datos (Forwarders / HEC) 
	• Gestión de KOs y búsquedas

**Opciones de ingestión** 
	• HEC (HTTP Event Collector) 
	• Apps de Splunkbase 
	• Conectores cloud (AWS, GCP, Azure)

### **Buenas prácticas**

**Para cualquier entorno** 
	• Separar roles (no juntar search head e indexer).
	• Usar forwarders (evitando recolectar datos desde indexers). 
	• Almacenamiento SSD en indexers. 
	• Red ≥ 1 Gbps; ideal 10 Gbps en clusters. 
	• Evitar usar Heavy Forwarders salvo necesidad clara. 
	• Documentar configuraciones y pipelines.

**Escalabilidad** 
	• Escalar indexers horizontalmente cuando crece la ingesta. 
	• Escalar search heads cuando aumentan usuarios o búsquedas programadas.