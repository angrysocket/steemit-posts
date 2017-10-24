# <center> **Deshabilitar IPv6 en Debian Stretch** </center> #
---
* ### *IPv6 disable --> /etc/sysctl.d* ###

**ipv6-disable.conf**

Nos hacemos un script que deshabilita IPv6 en **todas las interfaces de red**. Puedes añadir cada interfaz por separado, pero con esto es suficiente.

```bash
net.ipv6.conf.all.disable_ipv6 = 1
```
Deshabilitar IPv6 en una interfaz específica, por ejemplo **eth0**

```bash
net.ipv6.conf.
```
