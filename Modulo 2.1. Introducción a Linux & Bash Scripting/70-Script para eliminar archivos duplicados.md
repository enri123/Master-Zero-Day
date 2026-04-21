fdupes . nos muestra todos los archivos duplicados del directorio actual.
Si no sabemos si tenemos instalados fdupes, podemos ejecutar command -v fdupes para comprobarlo.
![[Pasted image 20260311173138.png]]

Hacemos un fdupes para obtener los archivos duplicados, y le eliminamos el ./ del comienzo usando sed.
fdupes -r lista los duplicados de forma recursiva
![[Pasted image 20260311173650.png]]

