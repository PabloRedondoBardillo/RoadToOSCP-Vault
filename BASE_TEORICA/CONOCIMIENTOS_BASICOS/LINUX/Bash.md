
### Metacaracteres

**NO SON REGEX**

```bash 
.
```
Significados:
* Nombre.Extension
* Directorio actual (.)
* Directorio padre (..)
* .Nombre (Fichero oculto)

```bash 
*
```
Cualquier secuencia de caracteres incluso la nula

```bash 
?
```
Un caracter cualquier (obligatoriamente uno)

```bash 
[abcde]
```
Uno de los caracteres especificados

```bash 
[^abcde]
```
Uno caracter cualquiera menos los especificados

```bash 
[a-z]
```
Uno de los caracteres del rango (solo minusculas) Sin ñ

```bash 
[A-Z]
```
Uno de los caracteres del rango (solo mayusculas) Sin Ñ

```bash 
{x, y, z, ...}
```
Se generan todos los valores posibles

### Scripting

* Cada linea es un comando de bash
* Los comentarios son de la forma: *# Comentario*
* Se pueden poner varios comandos separados por *;* en la misma linea
* Si un comando es muy largo se puede partir en dos lineas usando *\\*

**SHEBANG**
```bash 
#!/bin/bash
```
Se utiliza para decirle al sistema operativo que interprete debe utilizar

**VARIABLES**
```bash 
<variableLocal>=<valor>
readonly <variableLocalConstante>=<valor>
```
No puede haber espacios ni antes ni despues del igual, tiene que ir todo seguido. Con *readonly* hacemos una variable constante

```bash 
unset <variable>
```
Eliminamos la variable

```bash 
export <variable>
```
Convertimos una variable local en una de entorno

Algunas variables de entorno famosas son:
* *PATH* Contiene una lista de directorios donde el sistema operativo busca ejecutables
* *HOME* Ruta absoluta del directorio de inicio
* *PWD* Ruta absoluta del directorio actual
* *OLDPWD* Ruta absoluta del anterior directorio de trabajo
* *USER* Nombre de usuario
* *SHELL* Ruta absoluta de la shell que se este utilizando
* *UID* Identificador unico y numerico del usuario actual

```bash 
$<variable>
```
Se usa el contenido de la variable

**ARGUMENTOS**
```bash 
$@
```
Lista de todos los argumentos

```bash 
$#
```
Numero de argumentos pasados

```bash 
$0, $1, ..., $9, ${10}, ...
```
El *$0* es el nombre del archivo, el resto son argumentos pasados despues de el

```bash 
shift
```
Desplaza los argumentos una posicion

**SUSTICION DE COMANDOS**
```bash 
<variable>=$(<comando>)
```
De esta manera el resultado del comando se almacena en una variable

```bash 
comando [opciones] $(<comando>)
```
No es necesario crear una variable siempre con el valor del comando, podemos incrustarlo donde lo necesitemos

**ENTRECOMILLADO**
```bash 
`<comando>`
```
Alternativa a *$(\<comando>)*

```bash 
"<cadenaDeCaracteres>"
```
Admite interpolacion (se pueden sustituir comandos y variables)

```bash 
'<cadenaDeCaracteres>'
```
No admite interpolacion, es el resultado literal del contenido

**DEPURACION DE SCRIPTS**
```bash 
bash -x <script>
```
Ejecuta el script mostrando cada comando que se va a ejecutar expandido

```bash 
bash -n <script>
```
Comprueba la ejecucion sintactica del script (no lo ejecuta)

```bash 
#!/bin/bash -x
set -x
```
Son equivalentes y alternativas a los comandos anteriores

**SENTENCIA FOR**
```bash 
for <variable> in <listaValores>
do
	<listaComandos>
done
```
Recorre cada uno de los elementos de la lista de valores. La lista de valores puede ser de la forma *<directorio/\*>*

**SENTENCIA CASE**
```bash 
case <cadena> in 
<patron1>) <listaComandos1>
		;;
<patron2>) <listaComandos2>
		;;
...
<patronN>) <listaComandosN>
		;;
esac
```
Estos patrones pueden usar metacaracteres [[Bash#Metacaracteres]], no Regex

**SENTENCIA IF**
```bash 
if <comando1>
then
	<listaComandos1>
elif <comando2>
	<listaComandos2>
else
	<listaComandos3>
fi
```
La sentencia *if* no comprueba una condicion, sino el resultado del estado de un comando. Es importante saber que en bash si un comando termina bien entonces lo hace con un codigo *0*. Para probar condiciones podemos usar *test*:

```bash 
if test <condicion>
	<listaComandos>
fi
if [ <condicion> ]
	<listaComandos>
fi
```
Esas dos sentencias *if* hacen lo mismo. Notar que los espacions entre los *\[]* son obligatorios. Para las condiciones tenemos distintos tipos de operadores. Notar que los espacios en blanco que se dejan entre operadores son obligatorios.

Si es un fichero:
```bash 
if [ <operador> <fichero> ]
	<listaComandos>
fi
```
Ese operador puede ser:
* *-f* Existe el fichero y es un fichero
* *-d* Existe el directorio y es un directorio
* *-s* Existe el fichero y tiene tamanno > 0
* *-r* Existe el fichero y el usuario tiene permiso de lectura
* *-w* Existe el fichero y el usuario tiene permiso de escritura
* *-x* Existe el fichero y el usuario tiene permiso de ejecucion

Si es una cadena:
```bash 
if [ <operador> "<cadena>" ]
	<listaComandos>
fi
if [ "<cadena1>" <operador> "<cadena2>" ]
	<listaComandos>
fi
```
Las comillas son obligatorias
El operador en el primer caso puede ser:
* *-z* Cadena de longitud 0
* *-n* Cadena de longitud distinta de cero
* *Nada* Es lo mismo que *-n*
El operador en el segundo caso puede ser:
* *=* Cadenas iguales
* *!=* Cadenas diferentes
* *\\<* Cadena1 antes que Cadena2
* *>* Cadena1 despues que Cadena2

Si es un numero:
```bash 
if [ <numero1> <operador> <numero2> ]
	<listaComandos>
fi
```
Ese operador puede ser:
* *-eq* Numero1 igual a Numero2
* *-ne* Numero1 distinto a Numero2
* *-gt* Numero1 mayor a Numero2
* *-lt* Numero1 menor a Numero2
* *-ge* Numero1 mayor o igual a Numero2
* *-le* Numero1 menor o igual a Numero2

Existen operadores de composicion (comunes para todos los tipos)
* *!* Negacion
* *-a* And
* *-o* Or


**SENTENCIAS**
Todas las sentencias son comandos y su salida se redirige al *stdout*, se pueden redirigir de otra manera, con *>* o *|*

