
### Ayuda

```bash 
man [comando]
```
Para obtener detalles de un comando

```bash 
info [comando]
```
Para obtener detalles de un comando

```bash 
apropos [temaEnIngles]
```
Muestra comandos relacionados con el tema

### Informacion del Entorno

```bash 
whoami
```
Para ver que usuario estamos utilizando en el sistema

``` bash
id
```
Para ver informacion del usuario que esta siendo usado, grupos...

``` bash
pwd
```
Para ver la ruta absoluta en la que nos encontramos

``` bash
hostname [nombre]
```
Mostrar el nombre hostname, el nombre es opcional, si se especifica hay que poner algun parametro para averiguar dicha informacion
* *-a* Para ver los alias del hostname
* *-i* Para ver las direcciones ip asociadas al hostname

``` bash
neofetch
```
Para mostrar el logo de Arch

``` bash
uname
```
Ver el tipo de so en el que estamos
* *-a* Muestra toda la informacion disponible
* *-r* Muestra la informacion del kernel
* *-m* Muestra la arquitectura del hardware

### Terminal

``` bash
alias nombre=comando
```
Crea un atajo para un comando, para hacerlo permanente: *~/.zshrc*

``` bash
unalias ll
```
Elimina un alias

``` bash
history
```
Muestra el historico de comandos
* *-c* Borra el historial de la terminal actual

``` bash
!n
```
Repite un comando con numero n segun el historial

``` bash
clear
```
Limpia la pantalla o *ctrl + l*

``` bash
xargs comando
```
Sirve para concatenar comandos, coge el resultado del comando anterior y lo transforma en argumentos para el nuevo comando

``` bash
env
```
Muestra todas las variables de entorno actuales
* *-i script* Ejecuta un script de forma aislada (sin acceso a variables de entorno)

``` bash
export variable=contenido
```
Permite crear y actualizar variables de entorno, para que los cambios sean permanentes: *~/.zshrc*
* *-p* Muestra todas las variables de entorno con la palabra *export* delante

### Internet

``` bash
ip (opcion) objeto [comando]
```
Se puede elegir una de los siguientes objetos:
* *a, address*  Para ver las interfaces del protocolo IP
* *netconf* Para ver la configuracion de las interfaces de red IP
* *neighbour* Para listar tus vecinos conocidos
* *l, link* Para ver el estado de ls interfaces de red
* *r, route* Para ver la tabla de rutas actual
Podemos modificar todos los datos obtenidos de los parametros anteriores, ejemplos de uso:

*sudo ip address add/del ip/mask dev interfaz*
Para poner/quitar una direccion ip a una interfaz

*sudo ip link set dev interfaz up/down*
Para encender/apagar una interfaz

*sudo ip route add/del default via ip dev interfaz*
Para poner/quitar una puerta de enlace por defecto

``` bash
wget url
```
Descarga el archivo de una url
* *-O archivo* Para ponerle un nombre al archivo
* *-P ruta* Para guardarlo en una ruta especifica
* *-c* Para reanudar una descarga interrumpida
* *-b* Para descargar en segundo plano
* *-r* Para descargar de forma recursiva un directorio entero
* *--no-parent* Para evitar que suba por carpetas anteriores en *-r*

``` bash
curl url
```
Muestra por la terminal el contenido extraido de la url
* *-o archivo* Para descargar y poner nombre al archivo
* *-O* Para descargar con el nombre por defecto del archivo
* *-L* Para continuar con la redireccion de la url y no te devuelva el codigo de estado
* *-I* Para solo descargar las cabeceras
* *-X metodo* Para especificar el metodo HTTP
* *-d informacion* Para enviar datos en una peticion
* *-H cabecera* Para usar una cabecera en concreto 

``` bash
ping url
```
Utiliza el protocolo ICMP enviando paquetes echo
* *-c n* Limita el numero de paquetes (n)
* *-i n* Controla la velocidad de paquete por segundo (n)
* *-t n* Limita el ttl (n)
* *-W n* Limita el tiempo de espera (n)

``` bash
nc [IP] [puerto]
```
Lee y escribe datos a traves de conexiones de red por TCP/UDP, muy util convinar con redirectores
* *-v* Verbose
* *-l* Poner un puerto en escucha
* *-z* Escanear puertos
* *-n* No DNS
* *-w* Limita el tiempo de ejecucion
* *-u* Modo UDP
* *-p* Especifica el puerto local

``` bash
ssh usuario@(IP/dominio) [comando]
```
Para conectarse de forma remota a otro dispositivo, si no se especifica comando te devuelve una bash
* *-p puerto* Para especificar el puerto
* *-i clave* Para conectarte usando una clave privada

``` bash
scp orgien destino
```
Origen/Destino pueden vale una ruta de nuestro sistema o una del otro usuario@(IP/dominio):ruta, copia archivos entre ordenadores
* *-P puerto* Para especificar el puerto
* *-r* Para copiar directorios de forma recursiva

### Exploracion y Busqueda

``` bash
ls [ruta]
```
Para listar el contenido de una carpeta, es opcional ruta
* *-l* Para ver los permisos (formato largo)
* *-a* Para ver los archivos ocultos

``` bash
find ruta -name nombre
```
Para buscar un archivo en un directorio
* *-name nombre* Para buscar un archivo con ese nombre
* *-iname nombre* Para buscar un archivo con ese nombre sin que importen las mayusculas
* *-type tipo* Para buscar por un tipo de archivo
* *-size tamano* Para buscar por tamano de archivo (+/-)(c,k,M,G)
* *-exec comando* Para ejecutar un comando por cada archivo encontrado
* *-maxdepth profundidad* Para especificar la profundiad en subdirectorios
* *-perm numero* Para buscar por permisos
* *-group grupo* Para buscar por grupo
* *-user usuario* Para buscar por usuario
* *-nogroup* Para buscar por aquellos que no tengan grupo
* *-nouser* Para buscar por aquellos que no tengan usuario
* *-o* OR logico

``` bash
file archivo
```
Para ver el tipo de contenido de un archivo segun los magic numbers

``` bash
echo "cadena", echo $variable, echo $(comando)
```
Para mostrar una cadena o variable del sistema o resultado de un comando

### Gestion de Archivos y Directorios

``` bash
cd [ruta]
```
Para cambiar el directorio de trabajo actual, si no se asigna una ruta vuelve a ~

``` bash
rm archivo/ruta
```
Para eliminar un archivo y directorios
* *-r* Para eliminar directorios con contenido, recursiva

``` bash
touch archivo
```
Modifica los datos de acceso al archivo, si no existe lo crea
* *-a* Cambia solo el tiempo de acceso
* *-m* Cambia solo el tiempo de modificacion
* *-c* No crea archivos
* *-t* Especifica la fecha de un archivo ((CC)YY)MMDDhhmm(.ss)

``` bash
mkdir ruta
```
Crea una ruta
* *-p* Crea directorios de padres segun lo necesite nuestra ruta

``` bash
cp rutaOrgien rutaDestino
```
Copia de la rutaOrigen a la rutaDestino
* *-r* Para copiar carpetas de forma recursiva
* *-i* Para darte la opcion de sobrescribir los archivos con el mismo nombre
* *-p* Para mantener los metadatos
* *-a* Hace *-r*, *-p*, y no rompe los enlaces simbolicos
* *-v* Verbose

``` bash
mv rutaOrgien rutaDestino
```
Mueve y renombra de la rutaOrigen a la rutaDestino
* *-i* Para darte la opcion de sobrescribir los archivos con el mismo nombre
* *-n* No sobrescribir nunca
* *-b* Hace una copia de seguridad automatica
* *-v* Verbose

``` bash
ln rutaOrigen rutaDestino
```
Crea un enlace entre dos archivos, por defecto: hardLink
* *-s* Crea un softLink

``` bash
rsync rutaOrigen rutaDestino
```
Puede usarse a nivel local o nivel de red usando: usuario@(IP/dominio):ruta 
* *-h* Human-readable
* *-a* Copia de forma recursiva manteniendo los metadatods y los permisos intactos
* *-v* Verbose
* *-z* Comprime los datos
* *--delete* Para que los dos directorios sean espejos exactos
* *--progress* Para ver el porcentaje de proceso
### Lectura y Edicion de Archivos

``` bash
cat archivo
```
Para listar el contenido de un archivo
* *batcat* Un bat mejorado

``` bash
diff archivo1 archivo2
```
Para ver las diferencias entre dos archivos

``` bash
nano archivo
```
Para abrir y editar un archivo

``` bash
vim archivo
```
Para abrir y editar un archivo, ver [[NVim-Cheat-Sheet]]

``` bash
nvim archivo
```
Para abrir y editar un archivo con plugins, ver [[NVim-Cheat-Sheet]]

### Compresion y Descompresion

``` bash
tar [rutaDestino]
```
No reduce el tamano, solo unifica archivos
* *-c* Crear un archivo empaquetado
* *-x* Extraer un archivo empaquetado
* *-t* Listar el contenido sin extraer
* *-v* Verbose
* *-f* Especificar el nombre del archivo (se pone al final y es muy comun)
* *-z* Para comprimirlo
* *-J* Para comprimirlo mas
* *-C rutaDestino* Extraer en la rutaDestino

``` bash
zip archivo rutaDestino
```
Para comprimir archivos y directorios en formato *.zip*
* *-r* Comprime directorios de forma recursiva
* *-e* Para proteger con contrasena
* *-q* Modo silencioso
* *-n* Controla el nivel de compresion n=1 muy rapido, n=9 muy lento

``` bash
unzip archivo (archivoBuscado)
```
Para descomprimir archivos *.zip*, si se especifica el archivoBuscado solo se extraera dicho archivo
* *-d ruta* Para especificar la ruta de extraccion
* *-l* Listar el contenido sin descomprimir
* *-t* Comprobar si el archivo esta corrupto

``` bash
gzip archivo
```
Para comprimir archivos y haciendo que se eliminen
* *-k* Mantiene el archivo original y creo el otro nuevo
* *-r* Comprimir uno a uno los archivos de una carpeta
* *-n* Controla el nivel de compresion n=1 muy rapido, n=9 muy lento

``` bash
guzip archivo
```
Para descomprimir archivos y haciendo que se eliminen
* *-k* Mantiene el archivo original y creo el otro nuevo
* *-l* Listar el contenido sin descomprimir

``` bash
zcat archivo
```
Muestra el contenido de un archivo sin llegar a descomprimirlo y lo muestra por terminal

``` bash
7z comando archivo [directorio]
```
Para comprimir/descomprimir archivos 7z
* *a* Anadir a la compresion
* *x* Extraccion con rutas completas
* *e* Extrae todos los archivos sueltos y los mete en una carpeta
* *l* Listar el contenido sin descomprimir
* *t* Comprobar si el archivo esta corrupto
* *-p* Para proteger con contrasena
* *-mhe=on* Para proteger los nombres de los archivos del interior
* *-mxn* Controla el nivel de compresion n=1 muy rapido, n=9 muy lento
* *-vtamano* Divide la compresion en volumenes del tamano especificado

### Control de Flujo, Procesos y Operadores Logicos

``` bash
comando; comando
```
Concatenar comando, se ejecutan uno detras de otro

``` bash
comando && comando
```
Se ejecuta el segundo si el primero se ha ejecutado correctamente

``` bash
comando || comando
```
Se ejecuta uno de los dos, el primero que sea correcto

``` bash
comando &
```
Para abrir en segundo plano

``` bash
comando & disown
```
Para abrir en segundo plano sin ser dependiente de la terminal donde se ejecute

``` bash
comando | comando ...
```
Concatena el output de un comando con el siguiente

``` bash
ps
```
Muestra el estado de los procesos del sistema
* *a* De todos los usuarios
* *u* Muestra la informacion en formato orientado a usuarios
* *x* Muestra todos los procesos existentes (incluso los demonios)

``` bash
pgrep nombre
```
Muestra el PID del proceso con nombre

``` bash
top
```
Muestra todos los procesos del sistema y datos del sisteam en tiempo real

``` bash
htop
```
Como *top* pero con colores

``` bash
htop
```
Como *top* pero con colores

``` bash
kill PID
```
Envia una senal de proceso a traves de su PID, por defecto envia -15 (SIGTERM)
* *-9* SIGKILL
* *-l* Lista todos los nombres y numeros disponibles

``` bash
killall nombre
```
Mata a todos los procesos con exactamente ese nombre

``` bash
sudo systemctl accion servicio
```
Controla los servicios del ordenador (systemd)
* *status* Comprueba el estado del servicio
* *start* Arranca un servicio que estaba apagado (desaparece al reiniciar)
* *stop* Apaga un servicio activo
* *restart* Apaga y arranca un servicio que estaba activo
* *enable* Hace que el servicio arranque solo al encender el ordenador
* *disable* Quita el arranque automatico
* *--now* Forzar que se ejecute la accion en el momento
* *--failed* Mostrar que servicios han fallado en el arranque

``` bash
lsof [ruta]
```
Lista archivos abiertos y su proceso dentro de un directorio
* *-i [:p]* Muestra si un puerto o puertos estan usandose

``` bash
watch "comando"
```
Muestra el cambio sobre el resultado de repetir el mismo comando
* *-n n* Establece un intervalo de tiempo de ejecucion
* *-d* Resalta con color los cambios
* *-t* Quita la cabecera del sistema de ejecucion del propio comando

``` bash
free
```
Muestra el estado de la memoria RAM y Swap
* *-h* Human-readable

``` bash
crontab
```
Gestiona las tareas de cron
* *-l* Lista las tareas activas
* *-e* Abre el archivo de configuracion de cron
* *-r* Elimina todas las tareas de cron

``` bash
jobs
```
Muestra los procesos que se han pausado o enviado a segundo plano unicamente desde la terminal donde se ejecuta el comando
* *-l* Anade una columna con el PID del proceso
* *-p* Muestra unicamente los PIDs de los procesos
* *-r* Muestra solo aquellos que esta corriendo
* *-s* Muestra solo los pausados

``` bash
bg %n
```
Manda a segundo plano el trabajo numero n o *ctrl + z*

``` bash
fg %n
```
Manda a primer plano el trabajo numero n

### Gestion de Almacenamiento

``` bash
df
```
Da informacion sobre los discos/almacenamiento del sistema
* *-h* Human-readable
* *-T* Para ver el sistema de archivos
* *-t tipo* Para filtrar por un sistema de archivos

``` bash
du directorio
```
Da informacion sobre la capacidad de un directorio y todo su contenido interno
* *-h* Human-readable
* *-s* Para hacer un resumen
* *--max-depth profundiad* Para especificar la profundiad en subdirectorios

``` bash
sudo mount rutaOrigen rutaDestino
```
Monta una unidad logica en una ruta concreta para poder ser accedida
* *-o p* Especificar un parametro
* *p=ro* Modo solo lectura
* *p=noexec* Bloquea la ejecucion de scripts
* *p=rw* Modo lectura y escritura
* *p=remount* Permite cambiar las opciones de un disco si ya esta montado sin desmontarlo

``` bash
sudo umount ruta
```
Desmonta una unidad de una ruta para poder ser extraida

``` bash
lsblk
```
Muestra las unidades de almacenamiento y particiones
* *-f* Muestra el tipo de sistema de archivos y el UUID
* *-p* Fuerza a mostrar las rutas absolutas completas a los dispositivos
* *-o cols* Permite elegir solo las columnas que quieres separadas por comas

### Redirecciones y Descriptores de Archivos

``` bash
>
```
Para sustituir todo el contenido de un archivo

``` bash
>>
```
Para anadir contenido a un archivo

``` bash
comando &>/dev/null
```
Para redirigir el output entero de un programar (stdr 1,2) a la "nada"

``` bash
exec numero <> file
```
Para crear un descriptor de archivo de lectura (<) y escritura (>)

``` bash
exec numero>&-
```
Para eliminar un descriptor de archivo

### Administracion de Usuarios y Permisos

``` bash
su usuario
```
Para cambiar el usuario

``` bash
useradd nombre
```
Para crear un usuario
* *-s tipo* Para especificar la bash del usuario
* *-d ruta* Para especificar la ruta del directorio personal
* *-m* Para que se cree automaticamente el directorio personal
* *-g grupo* Para especificar el grupo principal del usuario (por defecto es su mismo nombre)
* *-G grupos* Para especificar los grupos secundarios del usuario
* *-c comentario* Para anadir un comentario al usuario
* *-e fecha* Para especificar una fecha en la cual se desactiva el usuario
* *-r* Para crear un usuario con permisos elevados

``` bash
userdel nombre
```
Para eliminar un usuario
* *-f* Fuerza la eliminacion del usuario
* *-r* Elimina el contenido de su directorio personal

``` bash
groupadd nombre
```
Para crear un grupo
* *-U usuarios* Para especificar los usuarios que van pertenecer al grupo

``` bash
groupdel nombre
```
Para eliminar un grupo

``` bash
chown propietario[:grupo] archivo/carpeta
```
Para cambiar el propietario, si especifica el grupo tambien se cambia

``` bash
chgrp grupo archivo/carpeta
```
Para cambiar el grupo

``` bash
chmod permisos archivo/carpeta
```
Para cambiar los permisos, ver [[Conceptos_teoricos#Permisos]]

``` bash
lsattr
```
Para ver permisos especiales, ver [[Conceptos_teoricos#Permisos]]

``` bash
chattr archivo
```
Para asignar permisos especiales, ver [[Conceptos_teoricos#Permisos]]

### Seguridad Avanzada (Capabilites)

``` bash
getcap archivo
```
Obtenemos las capabilities de un archivo
* *-r ruta* Para ver las capabilites desde un directorio de forma recursiva 

``` bash
setcap capability archivo
```
Para anadir una capability
* *-r archivo* Para eliminar capability

### Gestion de Paquetes

``` bash
sudo apt update
```
Para descargar las actualizaciones necesarias

``` bash
sudo apt upgrade
```
Para actualizar el sistema, **IMPORTANTE**: no usar sudo apt upgrade en parrot os

``` bash
parrot-upgrade
```
Para actualizar el sistema en parrot os

``` bash
sudo pacman -Syu
```
Para actualizar el sistema en Arch

``` bash
sudo yay/paru -Syu
```
Para actualizar el sistema en Arch utilizando AUR

### Procesamiento y Manipulacion de Texto

``` bash
grep "cadena" [archivo]
```
Para filtrar el contenido por una cadena en concreto en un archivo
* *-i* Ignorar mayusculas
* *-v* Filtro invertido, te muestra todo lo que no contiene
* *-r ruta* Busca de forma recursiva en un directorio
* *-o* Muestra unicamente las coincidencias (no la linea entera)
* *-n* Muestra el numero de linea exacto donde encontro la cadena
* *-w* Fuerza a que busque la cadena completa
* *-A n* Muestra la linea encontrada y n lineas despues
* *-B n* Muestra la linea encontrada y n lineas antes
* *-C n* Muestra la linea encontrada y n lineas antes y despues
* *-E o egrep* Para usar expresiones regulares avanzadas

``` bash
tail [archivo]
```
Para mostrar la ultima parte de un archivo
* *-n n* Para mostrar las n ultimas lineas, se puede usar (+/-)n
* *-f* Modo seguimiento (proceso) para que muestre cada vez que se actualiza el archivo y escribe la ultima linea
* *-c n* Para ver los ultimos n bytes

``` bash
head [archivo]
```
Para mostrar la ultima parte de un archivo
* *-n n* Para mostrar las n ultimas lineas, si anadimos -, entonces muestra todas las lineas menos las ultimas n
* *-c n* Para ver los primeros n bytes

``` bash
tr "conjunto1" ["conjunto2"]
```
Hace una sustitucion caracter a caracter, todos los primeros caracteres del primer conjunto se sustituyen por el primer caracter del segundo conjunto y asi sucesivamente
* *[:lower:]* Selcciona las minusculas 
* *[:upper:]* Selcciona las mayusculas
* *[:digit:]* Selcciona los numeros 
* *-d* Elimina todo un conjunto
* *-s* Elimina caracteres repetidos
* *-c* Invierte la seleccion en los conjunto

``` bash
sed 'opciones' [orden];[orden];... archivo
```
Ejecuta su orden sobre el archivo y lo devuelve por terminal(util para sustituciones y tratamiento de datos del archivo)
Las opciones pueden ser:
* *-i* Para que se guarden los cambios en el archivo
* *-i.end* Para que guarde los cambios en otro archivo
* *-E* Usa regex extendidas
* *-n* No muestra las lineas recorridas por defecto, importante ponerlo si solo se desea lo filtrado
Las ordenes son de la forma \[selector\]X\[argumentos\]
El selector puede ser:
* *N* Numero de linea
* *$* Ultima linea
* */patron/* Patron o regex
* *N,M* Rango numerico (desde la linea N hasta la M)
* */p1/,/p2/* Rango por patrones (desde que encuentra p1 hasta que encuentra p2)
* *N,/p/* Rango mixto (desde la linea N hasta que encuntra p)
* *inicio~salto* Salta desde el inicio las veces especificadas
* *\[orden\]!* Selector inverso
Si la X es:
* *p* Muestra lineas
* *d* Omitir/Borrar lineas
* *s* Sustitucion. Tiene como argumentos */busca/reemplaza/opciones/*. Las opciones pueden ser:
	* *g* reemplaza globalmente, todas las veces de la misma linea
	* *i* ignora mayusculas/minusculas
* *y* Reemplaza caracter a caracter. Tiene como argumentos */conjunto1/conjunto2*

``` bash
awk 'patron{accion}' archivo
```
Para procesar patrones, ideal para extraer columnas
* *'{print $n}'* Muestra el argumento n
* *'{print $NF}'* Muestra el ultimo argumento
* *-F separador* Especificar el separador de argumento (por defecto el espacio)

``` bash
cut archivo
```
Permite trabajar con archivos de texto plano con formato de "tabla" o con separadores
* *-d"delimitador"* Establece el delimitador, por defecto \t
* *-fN* Extrae el campo N (numero) 

``` bash
sponge archivo
```
Para absorber toda la entrada antes de escribirla y que el archivo no quede vacio al usar pipes y redirecciones al mismo archivo que se modifica

``` bash
rev
```
Le da la vuelta a una cadena

``` bash
sort archivo
```
Ordena
* *-n* Por numeros
* *-r* En orden inverso
* *-k n* Por una columna en concreto

``` bash
uniq
```
Elimina lineas repetidas si estan seguidas
* *-c* Muestra cuantas veces se repite una linea
* *-d* Muestra solo las lineas duplicadas
* *-u* Muestra solo las lineas que no estaban duplicadas

``` bash
wc archivo
```
Cuenta
* *-l* Lineas
* *-w* Palabras
* *-m* Caracteres

``` bash
tee archivo
```
Junto con una pipe, muestra por terminal y lo almacena en un archivo
* *-a* Lo anade en lugar de sustituir

