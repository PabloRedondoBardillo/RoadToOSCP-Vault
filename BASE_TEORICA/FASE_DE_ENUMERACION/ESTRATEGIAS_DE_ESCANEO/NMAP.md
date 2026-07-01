### Uso

``` bash
nmap [parametros] direccionIP
```

### Parametros

``` bash
-p[puertos]
```
Los puertos se pueden especificar mediantes comas: a,b,c o mediante rangos: a-b. Si se quiere especificar todo el rango de puertos basta poner -

Los puertos pueden estar en tres estados: abiertos, cerrados o filtrados

``` bash
--top-ports [x]
```
Para escanear los x puertos mas comunes

``` bash
--open
```
Para que devuelva puertos exclusivamente abiertos

``` bash
-v
```
Verbose

``` bash
-n
```
Para que no aplique resolucion DNS

``` bash
-T[n]
```
Para elegir la plantilla de temporizado

``` bash
-sT
```
Modo Stealth Scan, realiza un SYN, SYN ACK, RST

``` bash
-sV
```
Modo de deteccion de versiones

``` bash
-Pn
```
No verifica que el hosts este activo y por ello realiza el escaneo inmediatamente

``` bash
-sU
```
Para realizar un escaneo por UDP

``` bash
-sn
```
Para descubrir nuevos hosts (direcciones ip activas)

``` bash
--min-rate x
```
Cambia la velocidad de envio de datos, no mas lentos que x por segundo

### Evasion de firewalls

``` bash
-f
```
Para fragmentar paquetes

``` bash
--mtu [multiplo8]
```
Para especificar la cantidad de bytes a la hora de fragmentar peticiones, no se usa con *-f*

``` bash
-D [direccionesIP]
```
Para mandar solicitudes con distintas direcciones ip

``` bash
--source-port x
```
Para cambiar el puerto de origen a x (del equipo propio)

``` bash
--data-length x
```
Para configurar el tamano del paquete a x

``` bash
--spoof-mac (nombre o direccion)
```
Para mandar solicitudes con distintas direcciones mac

