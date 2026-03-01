Usamos find para encontrar archivos en una cierta rutas, en este caso . simboliza en el directorio en el que se encuentra, en el primer caso el archivo existe en la ruta seleccionada, por lo que lo muestra, en el segundo no existe, por lo que no muestra nada.
![[Pasted image 20260301123710.png]]

En este ejemplo usamos .., para que busque en la ruta anterior
![[Pasted image 20260301123808.png]]

En este caso / simboliza la raiz del sistema, al cual no tenemos acceso
![[Pasted image 20260301123853.png]]
Podemos usar 2>/dev/null para enviar los errores a una especie de agujero negro, y que no nos moleste
![[Pasted image 20260301123926.png]]
En este caso en lugar de los errores enviamos el output entero, usando >> /dev/null
![[Pasted image 20260301124009.png]]

Podemos usar junto a find, -type f para que busque en los ficheros
![[Pasted image 20260301124308.png]]

También podemos usar -type d para que busque los directorios
![[Pasted image 20260301124317.png]]

