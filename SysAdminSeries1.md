# <center> **Instalación de Debian cifrando el disco sobre LVM** </center> #
---

<center> **SysAdmin Series nº 1** </center>

---

## ¿Qué necesitamos? ##

Necesitamos un **USB**, con la capacidad necesaria para almacenar la imagen ISO de Debian, en este caso, utilizamos la versión **netinstall (amd64)**, que viene con lo mínimo, y la imagen ISO que puedes descargar desde [aquí](https://cdimage.debian.org/cdimage/buster_di_alpha1/amd64/iso-cd/debian-buster-DI-alpha1-amd64-netinst.iso) y el hash (SHA512) para verificarla desde [aquí](https://cdimage.debian.org/debian-cd/current/amd64/iso-cd/SHA512SUMS.sign)

## Preparación ##

Lo primero es montar la imagen.iso en el USB. Para ello debes tener privilegios **root**

```bash
dd if=/ruta/a/la/imagen.iso of=/ruta/al/usb
```

por ejemplo

```bash
dd if=/home/XXX/descargas/imagen.iso of=/dev/sdb1
```


Si quieres ver el progreso, puedes utilizar **pv** 

```bash
dd if=/ruta/a/la/imagen.iso |pv| dd of=/dev/sdbX
```

## Instalación ## 


