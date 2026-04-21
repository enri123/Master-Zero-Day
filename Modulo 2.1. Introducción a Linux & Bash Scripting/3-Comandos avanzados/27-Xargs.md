**xargs** es un comando de línea de comandos en sistemas Unix y Linux que **convierte la entrada estándar (stdin) en argumentos para otro comando**. Es especialmente útil cuando necesitas pasar una lista de elementos (como archivos, palabras o líneas) como argumentos a un comando que no acepta entrada directa, como `rm`, `cp`, `mkdir` o `tar`.

### Funcionamiento básico
- **Toma la salida de un comando** (por ejemplo, `find`, `grep`, `ls`) y la usa como argumentos para otro comando.
- Por defecto, **divide la entrada por espacios y saltos de línea**, lo que puede causar problemas si los nombres de archivos contienen espacios o caracteres especiales.
- Usa la opción **`-0`** junto con `-print0` en `find` para manejar nombres de archivos con espacios, comillas o saltos de línea correctamente.

### Ejemplos comunes
- **Eliminar múltiples archivos**:
  ```bash
  find /path -name "*.log" | xargs rm
  ```
- **Crear directorios desde una lista**:
  ```bash
  echo "dir1 dir2 dir3" | xargs mkdir
  ```
- **Archivar archivos con extensión .txt**:
  ```bash
  find . -name "*.txt" -print0 | xargs -0 tar -cvf archive.tar
  ```
- **Procesar cada línea con un comando personalizado** usando `-I`:
  ```bash
  find . -name "*.sh" | xargs -I {} cp {} ~/backup/
  ```


En este ejemplo, lo que estamos haciendo es mover todos los ficheros que terminen en .txt a una carpeta llamada backup
![[Pasted image 20260301125904.png]]

En este otro ejemplo lo que estamos haciendo es a los ficheros que terminan en .txt añadirles al final .bak
![[Pasted image 20260301125946.png]]

Como podemos ver en este ejemplo también se lo podemos añadir al principio
![[Pasted image 20260301130003.png]]

