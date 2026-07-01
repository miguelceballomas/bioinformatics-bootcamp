## Metaarácteres útiles para trabajar en bash
Continuando con el uso de `"`, conviene usarlo a la hora de llamar cualquier variable, ya que si la variable a la que llamas por ejemplo contuviese espacios podría dar errores de redirección, por ejemplo:
`f = 'mi texto.txt'`, esto estaría bien, pero si pusiésemos luego
` echo 'informe del día' > $f`, nos daría error, ya que el terminal expandiría `f` y separaría mi y texto.
` echo 'informe del día' > "$f"`, poniéndolo entrecomillado, bash tratará 'mi texto.txt' como una unidad pero sin tomarlo literal como si lo pusiesemos entre comillas simples `'` .

Para los ficheros se pueden usar ciertos metacarácteres para ahorrar pulsaciones de teclas para hacer coincidir nombres de archivos:
- `*` Coincide con cualquier cantidad de carácteres, incluyendo cero. Ejemplo: `ls *.fastq` mostrará todoso los ficheros que terminen en .fastq
- `?`: Coincide exactamente con un carácter. Por ejemplo: `ls sample?.fq` coincide con _sample1.fq_ pero no con _sample10.fq_
- `[...]` coincide con cualquiera de los caracteres listados o con cualquiera dentro de un rango. Ejemplo: `ls sample.fq` encuentra sample1.fq y sample2.fq; `ls chr[1-9].fa` encuentra chr1.fa..chr9.fa.
- `[!...]` o `[^...]` coincide con cualquier carácter que **NO** esté en la lista (negación). Ejemplo: ``ls sample[!0-9].fq`` listará ficheros cuyo carácter en esa posición no sea un dígito.

### Metacarácteres de redireccionamiento
Los comandos reciben datos desde la entrada estándar y envían resultados a la salida estándar. Los metacarácteres de redireccionamiento sirven para hacer las tuberías (pipes), con las que se puede pasar la salida de un comando como entrada de otro. También se pueden usar los símbolos `<` y `>` para leer datos desde archivos o guardar la salida en archivos.
- `<` dirige el contenido de un archivo al comando; suele ser la entrada estándar y `less < seq.fa` equivale a `less seq.fa`.
- `>` envía la salida estándar a un archivo y lo sobrescribe si ya existe.
- `2>` envía la salida de error estándar a un archivo.
- `&>` envía tanto la salida estándar como la de error estándar a un archivo.
- `>>` añade la salida al final de un archivo existente, en lugar de **sobrescribirlo**.


## Modificar texto de archivos txt
- La forma rápida es `echo "hola" > mi\ texto.txt`. Eso crea el archivo si no existe y mete dentro la línea `hola`. Si el archivo ya existía, _mayor que... simple_ `>` lo **sobrescribe** por completo. **Cuidado** con sobrescribir el archivo entero si no es lo que queremos.
- Para añadir sin sobrescribir, agregando el texto al final sin borrar lo anterior:`echo "otra línea" >> mi\ texto.txt` , usar  _mayor que... doble_  >>`>>` añade al final en vez de reemplazar el texto original.
- Para escribir manualmente lo más cómodo es usar un editor de texto como ``nano``, `nano mi\ texto.txt`. Se abre un editor en la terminal; escribes, y sales con `Ctrl+X`.
- Usando `cat`. 
	- Con la línea  `cat > mi\ texto.txt` puedes escribir directamente en la terminal. Cuando termines, pulsas `Ctrl+D` para guardar y salir. **Cuidado**, porque al igual que con el primer ejemplo, usar un solo signo `>` **sobresscribe** el texto. Podemos usar dos `>>` para agregar como antes
