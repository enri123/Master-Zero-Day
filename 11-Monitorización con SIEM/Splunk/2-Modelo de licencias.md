Splunk se licencia según el volumen de datos indexados por día.

Se mide en GB o TB por día.

 No importa el número de usuarios, la cantidad de búsquedas o dashboards... . Lo único que cuenta el cuánto volumen de logs entra al indexador cada 24 horas. 
 
 En Splunk Cloud se empieza a ofertar un modelo de licenciamiento por uso.

TIPOS DE LICENCIAS


| LICENCIAS GRATUITAS                          | ENTERPRISE                                        | CLOUD                                                              |
| -------------------------------------------- | ------------------------------------------------- | ------------------------------------------------------------------ |
| • Hasta 500MB/día.                           | Licencia clásica por volumen diario de ingesta.   | Mismo binario pero gestionado por Splunk en la nube.               |
| Sin funcionalidades potencialmente críticas. | Funcionalidad completa.                           | • El cliente paga por:                                             |
| Ideal para laboratorios o pruebas.           | Permite despliegues distribuidos, clustering... . | Volumen de datos diarios.                                          |
|                                              | • Entornos on-premise.                            | Capacidad de almacenamiento e infraestructura (Compute + Storage). |

Licencias gratuitas

Con la instalación de Splunk se activa la licencia de prueba (trial license). Limitaciones de la licencia de prueba: 
• Da acceso a todas las características de Splunk Enterprise.
• Sólo para instalaciones independientes, de una sola instancia de Splunk Enterprise. • No se puede apilar con otras licencias. 
• Expira 60 días después de instalar la instancia de Splunk. 
• Permite indexar 500 MB de datos por día. Si supera ese límite recibirá una advertencia de licencia.
• Se impide la búsqueda si hay un número determinado de advertencias de licencia (5 advertencias en un periodo de 30 días).

Pasados los 60 días la licencia se convierte en la licencia gratuita (free license). Limitaciones de la licencia gratuita: 
• Da acceso a un conjunto limitado de características de Splunk Enterprise. 
• Sólo para una instalación independiente, de una sola instancia de Splunk Enterprise. 
• No se puede apilar con otras licencias. 
• No caduca. 
• Permite indexar 500 MB de datos por día. Si supera ese límite recibirá una advertencia de licencia. 
• Se impide realizar búsquedas si hay varios avisos de licencia (3 advertencias en un periodo de 30 días).