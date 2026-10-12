## Permisos

Al listar el contenido con sus permisos de todos los archivos, directorios, links... Veremos una estructura a la izquierda del todo de este modo:

x xxx xxx xxx

El primer sector tipo de elemento: . (archivo), d (directorio), l (soft link), ...
El segundo sector permisos propietario (u): -rwx
El tercer sector permisos grupo (g): -rwx
El cuarto sector permisos otros (o): -rwx

r: permiso de lectura
w: permiso de escritura
x: permiso de ejecucion

**Forma octal**:
xxx xxx xxx
Cada grupo de tres forma un numero en binario, si el permiso en dicho grupo esta activo es un uno, de lo contrario un 0. El pasar el numero al formato decimal otorga el numero del grupo, la union consecutiva de estos forma un numero de tres digitos que es el numero octal del permiso.

Podemos anadir el **sticky bit** a la carpeta de tal modo que si tenemos una carpeta con mas permisos que un archivo contenedor entonces el archivo se cine a sus permisos no a los de la carpeta. Hay que tener cuidado ya que hace que los archivos previamente ejecutados se queden en memoria en vez de pasar a disco o cerrarse por lo que un uso excesivo puede saturar la memoria RAM local. Suele ser ejecutado sobre carpetas que manejen archivos temporales como /tmp o /var/tmp. Se aplica incorporando una t a los permisos o un 1 en octal.

Permiso **suid** se aplica incorporando una s a los permisos o un 4 en octal. Permite termer los permisos del usuario de forma temporal, de modo que al ejecutar un binario se ejecute como si el propietario lo estuviera haciendo.

Permiso **sgid** igual que el **suid** pero aplicado al grupo.

Una **capability** es un permiso especial otorgado a nivel de kernel en Linux que permiten dar privilegios especiales a ciertos binarios que normalmente tienen permisos unicamente para el usuario root. Una capability importante es **ep**.

Ver [[Comandos_basicos#Administracion de Usuarios y Permisos]]
## Directorios

**Raiz (/)**: directorio principal a partir del cual se ramifican el resto.

**/bin**: directorio estatico y compartible en el que se almacenan archivos binarios/ejecutables necesarios para el funcionamiento del sistema. Pueden ser usados por todos los usuarios del so.

**/boot**: directorio estatico y no compartible en el que se almacenan todos los archivos necesarios para el arranque del ordenador excepto los archivos de configuracion. Ejemplo el Kernel y el gestor Grub.

**/dev**: se almacenan los archivos que representan nuestros dispositivos de hardware:
* cdrom: CDROM
* sda: disco duro SATA
* audio: tarjeta de sonido
* psaux: puerto PS/2
* Ipx: impresora
* fd0: disquetera

**/etc**: directorio estatico que contiene la configuracion del so y de algunos programas. Algunos archivos pueden ir directamente en **/home** en vez aqui.

**/home**: directorio variable y compartible que contiene la totalidad de los archivos personales de los distintos usuarios del so a excepcion de root.

**/lib**: directorio estatico y puede ser compartible que contiene bibliotecas que son necesarias para ejecutar los binarios de **/bin** y **/sbin**.

**/mnt**: alberga los puntos de montaje de los dispositivos externos al ordenador como discos duros externos, particiones externas...

**/media**: alberga los puntos de montaje de los dispositivos externos al ordenador como usbs, disquetes, cd-rom...

**/opt**: directorio estatico y compartible que contiene los programas que no vienen con nuestro so.

**/proc**: sistema de archivos virtual que nos proporciona informacion sobre los procesos y aplicaciones que se estan ejecutando en el so.

**/root**: directorio variable y no compartible el cual funciona como el **/home** de root.

**/sbin**: directorio estatico y compartible, parecido a **/bin** pero contiene los binarios que solo puede ejecutar root. 

**/srv**: se usa para almacenar directorios y datos que usan ciertos servicios que podamos tener instalados en nuestro ordenador.

**/tmp**: donde se crean los archivos temporales del so.

**/usr**: directorio compartido y estatico que contiene la gran mayoria de programas instalados, su contenido es solo de lectura.

**/var**: contiene archivos de datos variables y temporales como logs, su funcion principal es poder corregir errores del so.

**/sys**: contiene informacion parecida a **/proc**, podemos encontrar todo nuestro kernel de forma estructurada.

**/lost-found**: contiene archivos y directorios que hayan sido recuperados tras la caida del so.

## Archivos Especiales

Si el nombre del archivo es *-* por lo que al hacer *cat -* parece que es un parametro, posbiles soluciones:
``` bash
cat ./-

cat ~/-

cat $(pwd)/-
```

Si el nombre del archivo contiene espacios en blaco por lo que al hacer *cat fi le* parece que abre dos archivos, posbiles soluciones:
``` bash
cat fi\ le

cat "fi le"
```

## TMUX

TMUX es una shell que permite lograr una agilidad por las terminales de forma impecable, aqui hay una lista de atajos muy utiles: ![[Tmux-Cheat-Sheet.pdf]]
## KITTY
Como Oh My Tmux pero mejorado, para ver su documentacion acceder: https://sw.kovidgoyal.net/kitty/overview/. Para ver un cheatsheet de comandos: 
![[Kitty-Cheat-Sheet]]

## NVIM
Editor de texto que mejora la velocidad de edicion del sistema. Una cheatsheet de comandos: 
![[NVim-Cheat-Sheet]]