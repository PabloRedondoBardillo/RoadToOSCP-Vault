
**NO SON METACARACTERES DE LA BASH**

```bash 
.
```
Un caracter cualquiera excepto el salto de linea

```bash 
*
```
El elemento precedente debe aparecer 0 o mas veces

```bash 
+
```
El elemento precedente debe aparecer 1 o mas veces

```bash 
?
```
El elemento precedente es opcional

```bash 
[ ]
```
Conjunto de caracteres admitidos (enumeracion o rangos con -)

```bash 
[^ ]
```
Conjunto de caracteres no admitidos (enumeracion o rangos con -)

```bash 
^
```
Principio de linea

```bash 
$
```
Fin de linea

```bash 
( )
```
Grupo de captura

```bash 
\n
```
Referencia a la n-esima expresion marcada

```bash 
|
```
OR

```bash 
\
```
Escape, permite indicar un metacaracter como un simbolo natural

```bash 
'\n'
```
Salto de linea

```bash 
'\t'
```
Tabulacion

```bash 
{n}
```
n ocurrencias de la expresion precedente

```bash 
{n,}
```
Al menos n ocurrencias de la expresion precedente

```bash 
{,m}
```
A lo sumo (o 0) m ocurrencias de la expresion precedente

```bash 
{n,m}
```
Al menos n y a lo sumo m ocurrencias de la expresion precedente

```bash 
[[:alpha:]]
```
Caracteres alfabeticos del locale (eng, esp, ...)

```bash 
[[:upper:]]
```
Caracteres alfabeticos en mayusculas

```bash 
[[:lower:]]
```
Caracteres alfabeticos en minusculas

```bash 
[[:digit:]]
```
Caracteres numericos [0-9]

```bash 
[[:xdigit:]]
```
Caracteres hexadecimales [0-9a-f]

```bash 
[[:alnum:]]
```
Caracteres alfanumericos

```bash 
[[:space:]]
```
Cualquier espacio en blanco y \t \r \n

```bash 
[[:punct:]]
```
Signos de puntuacion

```bash 
[[:graph:]]
```
Caracteres alfanumericos y signos de puntuacion

```bash 
[[:print:]]
```
Caracteres alfanumericos, signos de puntuacion y \[\[:space:\]\]

```bash 
[^[:x:]]
```
Negado de x

```bash 
\b
```
Comienzo o fin de palabra

```bash 
\B
```
Como \b pero la expresion no puede ni comenzar ni finalizar la palabra (tiene que estar metida dentro). Lo contrario de \b (no literalmente)

```bash 
\<
```
Unicamente comienzo de palabra

```bash 
\>
```
Unicamente fin de palabra

```bash 
\w
```
Cualquier caracter que pueda formar parte de una palabra

```bash 
\W
```
Lo contrario de \w

```bash 
\s
```
Lo mismo que \[\[:space:\]\]

```bash 
\S
```
Lo contrario de \s

