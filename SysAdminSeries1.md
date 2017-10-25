# <center> **CONFIGURANDO DEBIAN STRETCH DESDE 0** </center> #
---

<center> **SysAdmin Series nº 1** </center>

---

## Indice ##

* **1-** [Configuración de los repositorios](#)
  * **1.1-** [sources.list](#)
  * **1.2-** [sources.list.d](#)
     * [Virtualbox](#)
     * [Tor](#)
     * [Multimedia](#)
     * [Sublime](#)
	* [i2p](#)
	* [riot-web](#)

* **2-** [Firma de los repositorios](#)
  * [Virtualbox](#)
  * [Tor](#)
  * [Multimedia](#)
  * [Sublime-Text](#)
  * [i2p](#)
  * [riot-web](#)

* **3-** [Gestión de los paquetes y programas instalados](#)
  * **3.1-** [Eliminando programas y paquetes que no uso](#)
  * **3.2-** [Instalando programas y paquetes que nenecisto](#)
  * **3.3-** [Extensiones de Debian](#)

* **4-** [Customizando Debian](#)
  * **4.1-** [Paquete de iconos y tema Numix](#)
  * **4.2-** [Personalización del prompt](#)


---


<center> ![](https://s14-eu5.ixquick.com/cgi-bin/serveimage?url=http%3A%2F%2Ftheopensourcefeed.com%2Fassets%2Fimages%2Fpost-images%2FDebian%25209.png&sp=e35f94f08b133d28879c572c976e3210) </center>

Vamos darle una configuración inicial, por supuesto, es algo orientativo y podéis adaptarlo según vuestras necesidades y aplicarlo en cualquier sistema operativo basado en Debian.

## 1- Configuración de los repositorios ##

Lo primero que tenemos que configurar son nuestros sources.list, para ello incorporamos los de Debian Stretch a **/etc/apt/sources.list** y los externos a Debian en **/etc/apt/sources.list.d/** con el nombre **XXX.list**

### **1.1- sources.list**: ###

```bash
sudo nano /etc/apt/sources.list
```
Y lo modificamos con éste contenido:

```bash

### Debian Stretch Oficiales
deb http://ftp.es.debian.org/debian/ stretch main contrib non-free
deb-src http://ftp.es.debian.org/debian/ stretch main contrib non-free

### Debian Stretch Security
deb http://security.debian.org/debian-security stretch/updates main contrib non-free
deb-src http://security.debian.org/debian-security stretch/updates main contrib non-free

### stretch-updates, previously known as 'volatile'
deb http://deb.debian.org/debian stretch-updates main contrib non-free
deb-src http://deb.debian.org/debian  stretch-updates main contrib non-free

deb http://deb.debian.org/debian  stretch main contrib non-free
deb-src http://deb.debian.org/debian  stretch main contrib non-free

### Debian Stretch Backports
deb http://ftp.debian.org/debian stretch-backports main contrib non-free

###### Repositorio de Debian unstable, para descargar por ejemplo
###### la versión dev de Firefox, por default comentado.
#deb http://http.debian.net/debian  unstable main
```

**ctrl+o** (guardar) >> **ENTER** (confirmar el nombre del archivo) >> **ctrl+x** (salir)

Y ahora incorporamos los de las herramientas externas a Debian, para recibir las últimas actualizaciones y porque algunos directamente no se encuentran dentro de los repositorios de Debian.

### **1.2- sources.list.d**: ###

Vamos a utilizar el editor **nano**, pero podeis sustituirlo por vuestro editor preferido. También se puede automatizar todo este proceso en unn script en bash, en otro post, veremos como hacerlo.

 ```bash
 cd /etc/apt/sources.list.d
 ```

#### *Virtualbox* ####

```bash
nano vbox.list
```

Y copiamos los sources

```bash
# vbox deb stretch
deb http://download.virtualbox.org/virtualbox/debian stretch contrib
```

#### *Tor* ####

```bash
nano tor.list
```

Y copiamos los sources

```bash
## Tor
deb http://deb.torproject.org/torproject.org stretch main
deb-src http://deb.torproject.org/torproject.org stretch main
```

#### *deb-multimedia* ####

```bash
nano multimedia.list
```

Y copiamos los sources

```bash
## deb-multimedia
deb http://www.deb-multimedia.org stretch main non-free
```

#### *sublime-text* ####

```bash
nano sublime.list
```

Y copiamos los sources

```bash
## sublime-text
deb https://download.sublimetext.com/ apt/stable/
```

#### *i2p* ####

```bash
nano i2p.list
```

Y copiamos los sources

```bash
## i2p
deb https://deb.i2p2.de/ stretch-testing main
deb-src https://deb.i2p2.de/ stretch-testing main
```

#### *riot-web* ####

```bash
nano riot-web.list
```

Y copiamos los sources

```bash
## Riot (Matrix client)
deb https://riot.im/packages/debian/ stretch main
deb-src https://riot.im/packages/debian/ stretch main
```

Una vez tenemos nuestros sources.list preparados, vamos a incorporar las firmas de los externos. Si actualizasemos ahora, obtendríamos una pila de errores.

## 2- Firma de los repositorios ##

#### *Virtualbox* ####

```bash
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
```

Puedes ver más información sobre su instalación [aquí](https://www.virtualbox.org/wiki/Linux_Downloads)

#### *Tor* ####

```bash
gpg --keyserver keys.gnupg.net --recv A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89
```

```bash
gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -
```

```bash
sudo apt update
```

```bash
sudo apt install deb.torproject.org-keyring
```

Puedes ver más información sobre su instalación [aquí](https://www.torproject.org/docs/debian.html.en)

#### *deb-multimedia* ####

```bash
wget http://www.deb-multimedia.org/pool/main/d/deb-multimedia-keyring/deb-multimedia-keyring_2016.8.1_all.deb
```

```bash
dpkg -i deb-multimedia-keyring_2016.8.1_all.deb
```

```bash
rm -rf deb-multimedia-keyring_2016.8.1_all.deb
```

Puedes ver más información sobre su instalación [aquí](http://www.deb-multimedia.org/)

#### *sublime-text* ####

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

```bash
apt install apt-transport-https
```

Puedes ver más información sobre su instalación [aquí](https://www.sublimetext.com/docs/3/linux_repositories.html#apt)

#### *i2p* ####

```bash
wget -q https://geti2p.net/_static/i2p-debian-repo.key.asc -O- | sudo apt-key add -
```

Puedes ver más información sobre su instalación [aquí](https://geti2p.net/en/download/debian#debian)

#### *riot-web* ####

```bash
wget -q https://riot.im/packages/debian/repo-key.asc -O- | sudo apt-key add
```

Puedes ver más información sobre su instalación [aquí](http://data.agaric.com/how-install-riot-desktop-matrix-client-debian-based-systems)

## 3- Gestión de los paquetes y programas instalados ##

Aunque viene con los programas mínimos (también depende de lo que hayamos elegido durante la instalación) vamos a desinstalar los juegos y otros programas que, al menos para mí, son innecesarios. También instalaremos los paquetes, que en mi caso, son imprescindibles, aunque obviamente, no están todos, pero para que os hagáis una idea. Algunos de ellos son referentes a la tarjeta gráfica por ejemplo, por lo que muchos no lo necesitareis.

### 3.1- Instalación de programas y paquetes ###

```bash
apt -y update
```

Instalación de programas y paquetes:

```bash
apt -y install i2p i2p-keyring dmks sublime-text tor torsocks proxychains torbrowser-launcher apt-transport-https riot-web electrum vlc pidgin pidgin-otr apt-transport-https firmware-amd-graphics thermald pidgin pidgin-otr htop vlc arduino firmware-amd-graphics proxychains torbrowser-launcher virt-manager nmap curl aircrack-ng reaver hashcat virtualbox-5.1 sublime-text audacity keepassx python3-venv
```

### 3.2- Desinstalación de programas y paquetes ###

```bash
apt -y remove --purge PROGRAMASQUEQUIERASQUITAR
```

### 3.3- Extensiones de Gnome ###

```bash
sudo apt -y install gnome-shell-extension-dashtodock gnome-shell-extension-top-icons-plus gnome-shell-extension-weather
```

## 4- Personalizando nuestro Debian ##

### 4.1- Instalando el tema y paquete de iconos de Numix ###

```bash
apt -y install numix-gtk-theme numix-icons
```

### 4.2- Personalizando el prompt ###

Si queremos modificar el prompt para el usuario normal, hay que modificar el archivo **/home/XXX/.bashrc**. Si queremos modificar el del usuario root, modificamos el archivo **/root/.bashrc**

```bash
# user
PS1='${debian_chroot:+($debian_chroot)}\n\[$(tput bold)\]\[\033[38;5;10m\]\u\[$(tput sgr0)\]\[\033[38;5;15m\]@\h \[$(tput sgr0)\]\[\033[38;5;15m\] - \[$(tput sgr0)\][\[$(tput sgr0)\]\[\033[38;5;251m\]\t\[$(tput sgr0)\]]\[$(tput bold)\]\[\033[38;5;10m\]>>\[\033[38;5;68m\]  \w\[$(tput sgr0)\]\[$(tput bold)\]\[\033[38;5;15m\] \n \\$ \[$(tput sgr0)\]'
```

![](https://i.imgur.com/YykqIZi.png)


```bash
# root
PS1='${debian_chroot:+($debian_chroot)}\n\[$(tput bold)\]\[\033[38;5;196m\]\u\[$(tput sgr0)\]\[\033[38;5;15m\]@\h \[$(tput sgr0)\]\[\033[38;5;15m\] - \[$(tput sgr0)\][\[$(tput sgr0)\]\[\033[38;5;251m\]\t\[$(tput sgr0)\]]\[$(tput bold)\]\[\033[38;5;68m\]>>  \w\[$(tput sgr0)\]\[$(tput bold)\]\[\033[38;5;15m\] \n \\$ \[$(tput sgr0)\]'
```

![](https://i.imgur.com/rJ3wHfV.png)

Si queréis, antes de tocar los archivos directamente, podeis probar en un simulador online [aquí](http://bashrcgenerator.com/)
Hay otra manera de "colorear" el prompt, podéis verlo [aquí](https://stackoverflow.com/questions/4133904/ps1-line-with-git-current-branch-and-colors), más adelante explicaré en otro post el tema de los colores tanto para el prompt, como para los scripts.
