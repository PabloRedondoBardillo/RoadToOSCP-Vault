## Inicio

Si el teclado esta en espanol:
```bash 
loadkeys es
```

```bash 
archinstall
```

Una vez entrado en el menu de configuracion de archinstall:

1. Elegir el idioma
2. Elegir localidades -> distribucion de teclado / idioma local
3. Elegir espejos y repositorios (mas cercana)
4. **PARTICIONES**

Elegir particion manual

Si queremos un dualboot con Windows:

* Selecionar el disco deseado donde esta windows y lo marcamos con [#]
* Una vez dentro seleccionar la particion donde este el arranque de windows (aprox 100-500 mb)
* Darle unicamente a asignar punto de montaje en /boot/efi, guardar y salir
* Darle a la particion previamente creada para almacenar arch [[Reduccion_Disco]]
* Darle a wipe data y seleccionar como sistema de archivos ext4
* Volverle a dar a la particion donde instalamos arch y asignar punto de montaje en /
* Guardar y salir

Si queremos cifrado de disco:
* Entrar en el cifrado y poner la contrasena (no se puede olvidar)
* Volver a entrar y elegir la particion a encriptar (muy importante porque sino se encriptara todo el disco y por ello tambien windows)

5. Elegir bootloader y dejarlo en grub, **PONER EL UNIFIED KERNEL EN DISABLE**
6. Elegir kernels y marcar solo linux-zen
7. Elegir un hostname
8. Elegir authentication y elegir contrasena de root y crear un usuario (preferiblemente con permisos para hacerse root)
9. Elegir perfil y en desktop -> xorg
10. Volver a elegir perfil y ahora en controladores de graficos elegir el conveniente para graficas nvidia mejor usar la opcion de Nvidia (open kernel module)
11. Elegir configuracion de la red y dejar el default
12. Elegir zona horaria
13. Dejar el NTP en enabled

**UNA VEZ ACABADOS LOS PASOS LE DAMOS A INSTALAR DIRECTAMENTE, CUANDO ACABE HAY QUE DARLE A CHROOT (NO A REINICIAR)**

```bash 
pacman -S nano

pacman -S os-prober

nano /etc/default/grub
```
Editar y quitar [#] de *GRUB_DISABLE_OS_PROBER=false* y de *GRUB_ENABLE_CRYPTODISK=y*

```bash
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB

grub-mkconfig -o /boot/grub/grub.cfg

exit

reboot
```

Extraer el pen-drive de la instalacion y cambiar en la bios la prioridad del disco de arranque, pasar la opcion 1 a GRUB y la opcion 2 a WindowsBootLoader. Despues de eso deberia funcionar el dualboot.

Nos daremos cuenta de que necesitamos meter dos veces la contrasena de encriptacion para acceder a Arch, vamos a crear una archivo clave que autorice la entrada directa en Arch despues de haber metido la primera contrasena.

```bash
sudo dd bs=512 count=4 if=/dev/random of=/crypto_keyfile.bin iflag=fullblock

sudo chmod 000 /crypto_keyfile.bin

sudo cryptsetup luksAddKey /dev/nvme0n1p5 /crypto_keyfile.bin

sudo nano /etc/mkinitcpio.conf
```
Buscar la fila donde pone *FILES=()* y poner *FILES=(/crypto_keyfile.bin)*

```bash
sudo nano /etc/default/grub
```
Buscar la linea que pone *GRUB_CMDLINE_LINUX_DEFAULT="..."* y anadir al final del todo *cryptkey=rootfs:/crypto_keyfile.bin*

```bash
sudo mkinitcpio -P

sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Capa grafica

### Sistema de sesion del arranque

```bash
sudo pacman -S lightdm lightdm-gtk-greeter

sudo systemctl enable lightdm.service
```

### Sistema completo Gh0stzk
Para el sistema en general vamos a estar usando un repositorio de Github de Gh0stzk en concreto el de RiceInstaller

```bash
curl -LO https://gh0stzk.github.io/dotfiles/RiceInstaller

chmod +x RiceInstaller

./RiceInstaller
```
Hay que darle a que **No** cuando diga si queremos que instale NeoVim

Si tenemos dos monitores es posible que tengamos problemas para cambiar de escritorios y pasar el raton de un lado a otro:

Para poder pasar el rato de un monitor a otro:

Miramos que monitores tenemos conectados y decidimos por los nombres cual va en que posicion
```bash
xrandr | grep " connected"
```

Despues instalamos:
```bash
sudo pacman -S arandr

arandr
```
Colocamos los monitores arrastrandolos en la posicion que queramos y guardamos el archivio en la siguiente ruta *~/.config/bspwm/bin/* con nombre *arandr_config.sh*, **importante hay que darle permisos +x** 

```bash
sudo nvim ~/.config/bspwm/bspwmrc
```
Y anadimos al final que ejecute el archivo anterior de esta forma *"${HOME}/.config/bspwm/bin/arandr_config.sh"*, para que se vean los cambios ejecutar super + alt + r

Para solucionar la configuracion de las polybars:
```bash
sudo nvim ~/.config/bspwm/bspwmrc
```
Y anadimos en la configuracion:
* *bspc wc -0 _nombre_ _nombre_*
* *bspc monitor _nombre_ -d 1 2 3*
* *bspc monitor _nombre_ -d 4 5 6*
De este modo el monitor con los escritorios del 1 al 3 queda el primero y el segundo con los escritorios del 4 al 6. Un ejemplo de esta configuracion se encuentra en [[zshrc_dotfile.txt]].

Ahora tenemos que modificar el archivo del *rice* que estemos usando que se encarga de lanzar las polybars. Se encuentra en *~/.config/bspwm/rices/_rice_/*
```bash
sudo nvim ~/.config/bspwm/rices/_rice_/Bar.bash
```
Y sustituimos todo el codigo por algo como el que esta en [[Bar_bash.txt]]. **Importante ver que el Bar.bash tenga permisos +x**. Para recargar y ver todo hacemos super + alt + r

Fuera de la configuracion para dos monitores:

Solucionar posibles problemas de sonido:
``` bash
sudo pacman -S pipewire pipewire-pulse pipewire-alsa pipewire-jack wireplumber alsa-utils

alsamixer
```
Comprobar que debajo de cada columna pone OO (activado) en vez de MM (muteado). Despues activar pipewire
```bash
systemctl --user enable --now pipewire.service
systemctl --user enable --now pipewire-pulse.service
systemctl --user enable --now wireplumber.service
```
Instalamos una herramienta grafica utilizada por la polybar para detectar el sistema de sonido.
```bash
sudo pacman -S pavucontrol
```
Con esta herramienta seleccionamos el dispositivo de salida de audio dando click en el tick de la derecha del todo

Solucionar posibles problemas con internet (interfaz):
```bash
sudo pacman -S networkmanager network-manager-applet nm-connection-editor
sudo systemctl enable --now NetworkManager
```

Creando bloque de la polybar para nuestra direccion ip:
Anadimos al archivo *modules.ini* en *.config/bspwm/rices/_rice_/* el siguiente codigo:
```ini
[module/ip_address]
type = custom/script
interval = 2
exec = ~/.config/bspwm/bin/ethernet_status.sh
label-background = ${color.mb}
```
Ahora hay que anadirlo en la seccion *modules-left=...* del archivo *config.ini* que se encuentra en el mismo dirctorio que *modules.ini*. Falta crear script *ethernet_status.sh* localizado en *~/.config/bspwm/bin/* con el siguiente codigo:
```bash
echo "%{F#2495e7}󰈀 %{F#ffffff}$(/usr/bin/ip a | grep enp7s0 | tail -n 1 | awk '{print $2}' | sed 's/\/24//')%{u-}"
```
Es importante sustituir la interfaz de red por la propia local, en este caso es *enp7s0*.
Para ver el archivo completo ver [[ethernet_status_sh.txt]].

Ademas para dejar la polybar perfecta, ver el resto de la configuracion aplicada en [[modules_ini.txt]] y [[config_ini.txt]].

Polybar terminada, pasamos al bloqueo de pantalla:
```bash
sudo pacman -S i3lock imagemagick
```
Descargamos el repositorio i3lock-fancy de Github
```bash
git clone https://github.com/meskarune/i3lock-fancy.git
```
Toca configurar el atajo, en teoria el ejecutable se encuentra en */usr/bin/i3lock-fancy*, modificamos el archivo *sxhkdrc* localizado en *~/.config/bspwm/config/*. Para ver como se hace y otras configuraciones ver el archivo [[sxhkdrc.txt]].
Si tenemos dos monitores tenemos el icono del candado se vera entre los dos, para solucionar el problema:
```bash
sudo nvim /usr/bin/i3lock-fancy
```
Y comentamos la linea que carga el icono del candado, puede ser esta:
```bin
convert "$image" "${hue[@]}" "${effect[@]}" -font "$font" -pointsize 26 -fill "$bw" -gravity center -annotate +0+160 "$text" "$icon" -gravity center -composite "$image"
```
Y anadimos debajo esta:
```bin
convert "$image" "${hue[@]}" "${effect[@]}" "$image"
```
Para ver la configuracion completa ver [[i3lock-fancy.txt]].

Instalamos un calendario para la polybar:
```bash
sudo pacman -S gsimplecal

nvim ~/.config/bspwm/rices/_rice_/modules.ini
```
Sustituimos la linea del modulo date de label por esta *label = "%{A3:gsimplecal:}%time%%date%%{A}"*

### Terminal y nvim
Cambiamos la terminal a una kitty haciendo super + alt + t. Nos movemos a *.config/kitty/* y hacemos: 
```bash
rm -r *
```
Creamos el arhcivo *kitty.conf* e incorporamos dentro el contenido de [[kitty_conf.txt]]. Hacemos lo mismo con *color.ini* pero esta vez copiamos lo de [[color_ini.txt]]

Nos situamos en el escritorio personal y hacemos lo siguiente tanto para un usuario normal como para root:
```bash
git clone https://github.com/NvChad/starter ~/.config/nvim && nvim
```

Por otro lado otra vez para root y un usuario ejecutamos el siguiente codigo:
```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf

~/.fzf/install
```


## Herramientas
### Dependencias AUR
```bash
git clone https://aur.archlinux.org/paru.git

cd paru

rustup defualt stable

makepkg -si

cd ~

git clone https://aur.archlinux.org/yay.git

cd yay

makepkg -si
```

### Herramientas Hacking
```bash
sudo pacman -S sqlmap nmap masscan gobuster

paru -S aircrack-ng ffuf burpsuite nikto john hashcat hydra wireshark-qt tcpdump netcat metasploit exploitdb curl wget git jq python-pip hcxtools hcxdumptool bettercap sherlock impacket proxychains-ng ghidra radare2 gdb pwndbg binwalk foremost volatility3 steghide exiftool openvpn seclists caido
```
Dejar todas sus opciones por defecto

### Herramientas Alternativas
```bash
sudo pacman -S spotify discord man google-chrome htop lsof cronie rsync

paru -S obsidian moreutils zip unzip 7zip trash-cli neofetch 
```
## Rutas Importantes
Para ver todas las rutas utilizadas en este archivo u otras ver: [[Rutas_Importantes]]