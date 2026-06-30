# Apuntes Linux Día 2
## Gestión de ficheros
Para gestionar los ficheros son esenciales los siguientes comandos:
- `cd`: cambiar directorio. Si no se le añade ninguna opción, cambia al ==directorio de inicio== (abreviado como ~)
- `pwd`: imprimir el directorio de trabajo actual. Muy útil para saber en cada momento en que lugar del PATH estamos.
- `mkdir`: crear un nuevo directorio
- `rmdir`: eliminar un directorio ==vacio==
	- `rm -r`: eliminar el contenido de un directorio **NO** vacio
	- `rm`: eliminar ficheros
- `chmod`: cambiar permisos de un fichero o directorio
- `ls`: listar el contenido de un directorio
- `cp`: copiar un archivo
- `mv`: mover un archivo

Para verificar los permisos de un directorio (por ejemplo, uno creado poniendo `mkdir Test1`) se puede hacer de la siguiente forma: `ls -ld Test1`, dandonos como resultado: ``drwxr-xr-x 2 student student 4096 Jun 30 16:27 Test1``
donde la primera ==d== ya nos indica que es un directorio, y la parte de ==rwxr-xr-x== indica los permisos.
- las opciones ``-ld`` de la lista son para:
	- ``ls -l`` que el formato de lista sea de contenido ==largo (long)== 
	- `ls -d` que la información sean los metadatos del directorio en sí, no su contenido.

Para modificar el acceso a este directorio se debe utilizar `chmod 700 Test1`, y si volvemos a ejecutar el comando anterior de `ls -ld` veremos que ahora los permisos se ven tal que ==drwx------==

Es útil saber tambien que para desplazarnos a el directorio de inicio tenemos las opciones
- `cd`, ya mencionada antes
- `cd $HOME`, donde **$HOME** es una variable de entorno que almacena el nombre de el directorio de inicio (podemos verlo escribiendo `echo $HOME`)
- `cd ~`, la virgulilla a secas sirve para el nuestro directorio de inicio, pero se puede usar para directorios de otro tipo `cd ~ana`, si existe. (la virgulilla se escribe con ==Alt gr + 4==)

Para identificar directorios en shell también se utilizan mucho dos formas:
- Usar un punto `.` sirve para referirnos al directorio actual
	- Por ejemplo `ls .` lista el directorio en el que nos encontremos
	- Otro ejemplo `./script.sh` lo que hace es ejecutar el script.sh, que se encuentra en el directorio actual.
- Usar dos puntos `..` sirve para referirnos al directorio directamente encima del actual (==directorio padre==)
	- Por ejemplo `cd ..` = vas al directorio de arriba.
	- Otro ejemplo`ls ..` = ves el contenido del directorio padre.
	- Otro ejemplo`cd ../proyecto` = subes un nivel y luego entras en `proyecto`.
Otra variable de entorno es $**PWD** que al igual que $**HOME** es una variable de entorno, pero en este caso guarda el directorio de trabajo actual.

Para crear notas se puede usar `touch notas.txt`
Para moverse entre directorios es super útil usar el autocompletar con el Tab, para ello se puede mirar primero los directorios dentro del directorio actual usando `ls`, o simplemente poner ``cd `` y hacer ==doble Tab== y luego elegir el directorio que nos interese viendolo en la lista. (**Importante**, dejar un espacio despues del `cd `, sino el terminal querrá autocompletar el comando cd, no nos dirá los posibles directorios a donde saltar)

## Metaarácteres útiles para trabajar en bash
- ``\``: tambien conocido como _escape_, preserva el valor literal del siguiente carácter que sigue, con la excepción de la nueva línea:
	- Si por ejemplo se escribe `$ echo variable ; argumento`, el punto y coma actua como carácacter especial y no se va a imprimir el texto entero, da error de comando. Si se escribe `$ echo variable \; argumento`, ahí si se va a imprimir el texto `variable; argumento`, ya que el punto y coma se interpreta como valor literal, no como meta carácter.
	- Otro ejemplo es para crear documentos con espacios, ya que un espacio es un metacarácter que indica separación. Si escribes `touch mi texto.txt` y haces un `ls mi*txt`, da error porque no hay ningun documento guardado como `mi texto.txt`, sino que seria solo `texto.txt`. Para solucionarlo, se escribiria `touch mi\ texto.txt` y así el espacio se interpreta como carácter literal de espacio, no como metacarácter separador.
	- Tambien se pueden usar para concatenar lineas cuando el texto es muy largo y hay que bajar de línea
- `'`: Las comillas simples, tienen un valor similar al _escape_, ya que se preserva el valor literal que haya entre las dos comillas:
	- Podriamos crear el mismo archivo de antes poniendo `touch 'mi texto.txt'`
	- Tambien permite concatenar varias lineas que se encuentren representadas por diferentes mecanismos de citación.
- `"`: Las comillas dobles, preservan el valor literal del texto **excepto de $ ,\`,  .** Es útil para la interpolación de variables dentro de comillas dobles, ya que con comillas simples el resultado sería distinto:
	- ```
	  `qty = '5'
	  $  echo 'Este año he marcado $qty goles`
	  ```  
	  Da como resultado la frase "Este año he marcado $qty goles", pero si usamos comillas dobles:
	- ```
	  $  echo "Este año he marcado $qty goles"
	  ```
	  Da como resultado la frase "Este año he marcado 5 goles"