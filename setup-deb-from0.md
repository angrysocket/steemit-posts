# <center> **CONFIGURANDO DEBIAN STRETCH DESDE 0** </center> #
---

## Indice ##

* [Configuración de los repositorios](#)
 * [sources.list](#)
 * [sources.list.d](#)
   * [Virtualbox](#)
   * [Tor](#)
   * [Multimedia](#)
   * [Sublime](#)
	* [i2p](#)
	* [riot-web](#)

* [Firma los repositorios](#)
 * [Virtualbox](#)
 * [Tor](#)
 * [Multimedia](#)
 * [Sublime-Text](#)
 * [i2p](#)
 * [riot-web](#)

* [Gestión de paquetes y programas instalados](#)
 * [Eliminando programas y paquetes que no uso](#)
 * [Instalando programas y paquetes que nenecisto](#)
 * [Extensiones de Debian](#)

* [Customizando Debian](#)
 * [Paquete de iconos y tema Numix](#)
 * [Personalización del prompt](#)

---

Después del post anterior, en el que explicamos cómo instalar nuestro Debian cifrado, con LVM, hoy vamos a darle una configuración inicial, por supuesto, es algo orientativo y podéis adaptarlo según vuestras necesidades y aplicarlo en cualquier sistema operativo basado en Debian.

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

Guardar= ctrl+o , ENTER para aceptar el nombre del archivo, y SALIR= ctrl+x

Y ahora incorporamos los de las herramientas externas a Debian, para recibir las últimas actualizaciones y porque algunos directamente no se encuentran dentro de los paquetes de Debian.

### **1.2- sources.list.d**: ###

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

#### *Tor* ####

```bash

```

```bash

```

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

#### *sublime-text* ####

```bash
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
```

```bash
apt install apt-transport-https
```

#### *i2p* ####

```bash
wget -q https://geti2p.net/_static/i2p-debian-repo.key.asc -O- | sudo apt-key add -
```

#### *riot-web* ####

```bash

```

## 3- Gestión de paquetes y programas instalados ##
Instalación de programas y paquetes

```bash
apt -y update
```

Instalación de programas y paquetes:

```bash
apt -y install i2p i2p-keyring dmks sublime-text tor torsocks proxychains torbrowser-launcher apt-transport-https riot-web electrum vlc pidgin pidgin-otr apt-transport-https  
```
Desinstalación de programas y paquetes:
## 4- Personalizando nuestro Debian ##

Instalando el tema y paquete de iconos de Numix

```bash
apt -y install numix-gtk-theme numix-icons
```
