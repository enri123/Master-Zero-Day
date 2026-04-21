**Conceptos CLAVE**

**HOST**: Equipo (hostname o dirección IP) en el que se ha generado el evento. Este campo host es configurable por lo que en algunas instancias también se puede entender como el servidor de Splunk que ha recogido el evento. 

**SOURCE**: Identifica la fuente de un evento. En el caso de eventos monitorizados desde ficheros o directorios el campo source será el path completo al fichero. En el caso de una fuente de red, el campo source será el protocolo y puerto. 

**TIME** o timestamp: Representa el tiempo en el que se generó el evento. En el caso de que el evento con contenga un timestamp válido o Splunk no sea capaz de extraerlo automáticamente se asignará el momento de indexado como su timestamp. Splunk utiliza este timestamp para correlar los eventos por tiempo, para crear histogramas o para aplicar filtros de tiempo en las búsquedas.


---

**INDEX** o índice: El repositorio de datos en sí mismo. Cuando Splunk indexa los eventos en raw, los transforma en eventos buscables. Para esto crea una estructura de ficheros raw y tsidx. Todos estos ficheros son archivos planos.

Separar los eventos en índices distintos cumple principalmente tres funciones: 
- **Retención**: El periodo de retención se establece por índice. Todos los eventos de un mismo índice tendrán un mismo periodo de retención. Si el almacenamiento disponible nos impide tener el mismo periodo de retención para todos los eventos tendremos que separar los eventos en distintos índices con distintos periodos de retención.

- **Control de acceso**: No todos los usuarios necesitan acceder a la misma información. Separar los eventos en índices distintos permite configurar distintos niveles de acceso para los distintos usuarios.  

- **Performance**: Al dividir la información en índices y añadir este índice en la query mejora sustancialmente el performance de las búsquedas.


---

**SOURCETYPE**: Identifica la estructura de datos de un evento. El sourcetype determina como Splunk formatea los datos durante el periodo de indexado y de búsqueda. 

Definir el sourcetype no es estrictamente obligatorio pero es altamente recomendable. Si el sourcetype no está definido intentará entender automáticamente el evento y extraer parámetros como el timestamp, pero esto puede fallar. Definir el sourcetype nos evitará estas situaciones. 

No confundir sourcetype con formato. Dos elementos con un mismo formato pueden necesitar sourcetypes distintos. 

Ejemplo: 

- Fichero 1.csv : “time”,”source”,”destination”,”message” 

- Fichero 2.csv: ‘timestamp’;’dest’;’src’;’protocol’;’bytes’ 

El sourcetype definirá cómo se extraerán los campos, transformaciones sobre estos campos, alias, etc. Ambos ficheros de ejemplo usan comillas distintas, delimitadores distintos, tienen campos distintos y campos iguales en distinto orden. Necesitarán sourcetypes distintos para que Splunk entienda cómo trabajar con esta información.

---

**TIPOS DE BUSQUEDAS**

**Raw event searches**: Búsquedas que sólo recuperan eventos de un índice o índices, y se utilizan normalmente cuando se desea analizar un problema. Algunos ejemplos de estas búsquedas son: comprobación de códigos de error, correlación de eventos, investigación de problemas de seguridad y análisis de fallos. Estas búsquedas no suelen incluir comandos de búsqueda (excepto la propia búsqueda), y los resultados suelen ser una lista de eventos sin procesar.

SPL: BÚSQUEDA BÁSICA 

**Transforming searches**: Búsquedas que realizan algún tipo de modificación o cálculo estadístico sobre un conjunto de resultados. Se trata de búsquedas en las que primero se recuperan eventos de un índice y luego se pasan los eventos a uno o más comandos de búsqueda. Estas búsquedas siempre requerirán campos y al menos uno de un conjunto de comandos estadísticos. Algunos ejemplos son: obtener un recuento diario de eventos de error, contar el número de veces que un usuario específico ha iniciado sesión o calcular el percentil 95 de los valores de campo. 

SPL: BÚSQUEDA BÁSICA | TRANSFORMACIÓN [| TRANSFORMACIÓN O FILTRO]*