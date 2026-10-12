
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

