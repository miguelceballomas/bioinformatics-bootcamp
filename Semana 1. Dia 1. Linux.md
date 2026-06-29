# Apuntes Linux Dia 1

## Conceptos aprendidos
Antes de cada comando debe de estar puesto $ para que el terminal lo entienda como una orden
Existen comandos como: ``date``, o ``ls``.
Despues de los comandos se pueden incluir opciones (tambien llamados argumentos):
- Si por ejemplo quieres poner `$ ls -l -a -t` son 3 opciones de una sola letra que afectaran al comando ``ls`` que lo que hace es abrir una lista. Es lo mismo que poner `$ ls -lat`, las 3 opciones se aplicarán.
- Hay opciones que son palabras completas como `help`, y para evitar que el terminal lo interprete como 
`-h -e -l -p` lo que se hace es poner doble guión `--help` 

Para ejecutar comandos tienen que estar alojados en lo que se conoce como "path" del terminal. Se pueden ejecutar comandos fuera del path si conoces su ruta completa, por ejemplo: `/bin/date` (bin no es basura).
	Lo más oportuno suele ser tener almacenados los comandos en directorios conocidos, y esos directorios agregarlos a la variable del entorno del path de nuestro shell.
	El **path** consiste en una lista de directorios que se verifican secuencialmente para los comandos ejecutados. Se puede ver usando el comando `echo $PATH`
Para editar una línea de comando:
- flecha ⬆ para navegar entre los comandos ejecutados
- control + A para ir al principio de la linea
- control + E para ir al final
- control + F o flecha ➡, para movernos 1 posición
- control + D para borrar 
- control + Intro para ejecutarla


## Comandos
- `uname`: Muestra el tipo de sistema que se está ejecutando.
	- si se añade la opción `-a` (`uname -a`), se mostrará además el nombre del host y la versión del kernel.
- `date`: Imprime día, fecha y hora actuales.
	- aquí es interesante usar el comando ``--help`` para ver todas las opciones de customización del formato de salida, pero lo más importante es que justo antes del formato pongas `+` o sino linux no entiende lo que le pides. Ej: `date "+%d/%m/%Y %H:%M"`
- `history`: Permite recuperar el historial de todos los comandos ejecutados, útil por si necesitas usar un comando largo que ya has usado antes. Si pones `history 9`, por ejemplo, el historial tomará el rango del número que le pongas.
	- El comando `! n` te permite ejecutar un comando del historial (n sería el número que aparece a la izquierda en el historial de comandos)
	- El comando ``!!`` te permite ejecutar el último comando que has ejecutado
	- El comando `!?string?` permite ejecutar el último comando con un string dentro. **OJO**, si el comando es date por ejemplo, sería ``!?date?`` o similares, ==no poner literalmente string==. Lo bueno es que no requiere poner todo el comando, por lo que valdría `!?at?` por ejemplo.