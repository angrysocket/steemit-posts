# <center>**Arduino UNO (Generic) & lcd 2004A, conexión mediante i2c**</center> #
---
El conector de i2c, tiene 4 pines, y hay que conectarlo en analógico.  

## CONEXIONES: ##

* **GND** --> GND
* **VCC** --> 5v
* **SDA** --> Analógico 4
* **SCL** --> Analógico 5

*SDA*: se encarga de la transmisión de datos

*SCL*: es el reloj y lleva los pulsos de reloj, ya que i2c es síncrona. De esta forma se evita perder información.

## CÓDIGO ##
