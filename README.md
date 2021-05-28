# VPC-acceso-VNC 🔐
Este tutorial se enfoca en la configuración necesaria para habilitar el entorno gráfico de una VSI Linux en VPC. Es válido aclarar que esta configuración también se puede aplicar para una VSI Linux de infraestructura clásica. 

## Índice  📰
[Pre-Requisitos](#Pre-Requisitos-pencil)

[Paso 1. Datos de configuración](#Paso-1)

[Paso 2. Habilitar el entorno gráfico de una VSI Linux](#Paso-2)

[Paso 3. Acceder al entorno gráfico](#Paso-3)

## Pre-requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Crear una VSI linux en VPC (también puede ser en infraestructura clásica).
* Debe tener instalado en su máquina el programa **TightVNC Viewer**.

## Paso 1
### Datos de configuración ⚙
Para realizar la configuración del entorno gráfico de una VSI Linux, debe contar con los siguientes datos:
1. Contraseña:

> Nota 1: En caso de contar con una VSI Linux en VPC, debe realizar de forma previa la respectiva configuración para agregar una nueva contraseña. Para realizar esa configuración, revise los enlaces que aparecen en la sección de [Referencias](#Referencias-mag) de este repositorio  La ruta que le permite encontrar su VSI en VPC es Menú de Navegación → Infraestructura VPC → Instancias de Servidor Virtual.
>
> Nota 2: En caso de contar con una VSI Linux en Infraestructura Clásica, obtenga la contraseña. Para ello, en el menú de navegación de click en Infraestructura Clásica y posteriormente en el dispositivo que va a configurar. Luego de esto, de click en la pestaña contraseñas y guarde la contraseña.

2. IP:

> Nota 1: En caso de contar con una VSI Linux en VPC, la IP que se utilizará en este tutorial es la IP Flotante, la cual puede encontrar dentro de su VSI en la sección **Interfaces de red**.
>
> Nota 2: En caso de contar con una VSI Linux en Infraestructura Clásica, utilice la IP pública, la cual puede encontrar dentro de su VSI en la pestaña **Visión general** y la sección **Detalles de la red.**

## Paso 2
### Habilitar el entorno gráfico de una VSI Linux 🛠
Para habilitar el entorno gráfico de su VSI Linux, siga los pasos que se muestran a continuación:
1. Abra una ventana de *Windows PowerShell* en su máquina y establezaca una conexión vía SSH. Para ello, utilice el siguiente comando (coloque en \<IP> la IP pública o flotante según sea el caso):
``` 
ssh root@<IP> 
```
Una vez ejecute este comando se le solicitará que coloque la contraseña determinada en el [Paso 1. Datos de configuración](#Paso-1). Verifique que después de colocar la contraseña ya se encuentre dentro de la VSI. Su ventana de *Windows PowerShell* debe mostrar algo de forma similar a ``` root@nombre_vsi:~# ```

2. Posteriormente debe actualizar la lista de paquetes mediante el comando:
```
sudo apt-get update
```

3. Debe instalar el entorno de escritorio *Xface* con el comando:
```
sudo apt install xfce4 xfce4-goodies
```

4. Debe instalar dentro de su VSI en *Windows PowerShell* el TightVNC. Para ello coloque lo siguiente: 
```
sudo apt install tightvncserver
```

5. Una vez finalizada la instalación se realiza la configuración inicial del servidor VNC con el comando: 
```
vncserver
```

6. Luego, le pedirá introducir y verificar una nueva contraseña, la cual le permitirá acceder al entorno gráfico de su VSI Linux. Asigne una contraseña distinta a la determinada en el [Paso 1. Datos de configuración](#Paso-1) y guardela para utilizarla más adelante.

7. Despues de introducir una contraseña le saldrá como respuesta el siguiente anuncio  ``` Output Would you like to enter a view-only password (y/n)? ```. Como respuesta coloque ```n```.

8. Después de esto se debe detener la instancia del servidor VNC, para ello se escribe el siguiente comando: 
```
vncserver -kill :1
```

9. Se debe modificar el archivo *xstartup*. Antes de ello se realiza una copia de seguridad del original, con el comando: 
```
mv ~/.vnc/xstartup ~/.vnc/xstartup.bak
``` 

10. Se crea un nuevo archivo *xstartup* y se abre en el editor de texto. Para ello se escribe: 
``` 
nano ~/.vnc/xstartup
``` 

11. Dentro de este archivo se ingresan las siguientes líneas:
```
~/.vnc/xstartup
#!/bin/bash
xrdb $HOME/.Xresources
startxfce4 &
```
Guarde el archivo con ```Ctrl s``` y cierre con ```Ctrl x```

12. Para garantizar que el servidor VNC puede acceder al archivo que acabamos de crear, lo hacemos ejecutable mediante el comando: 
```
sudo chmod +x ~/.vnc/xstartup
```

13. Se debe reiniciar nuevamente el servidor con el comando: 
```
vncserver
```

14. Para finalizar, en su máquina ejecute el siguiente comando (recuerde colocar en \<IP> la IP pública o flotante según sea el caso): 
```
ssh -L 5901:127.0.0.1:5901 -C -N -l root <IP>
```
Cuando se le solicite ingresar una contraseña coloque la determinada en el [Paso 1. Datos de configuración](#Paso-1). Despues de ingresar la contraseña el proceso en la ventana se quedará cargando y usted habrá finalizado la configuración.

> Nota: Si su VSI Linux está en VPC, deberá agregar una regla de configuración que le permita utilizar el puerto 5901. Para ello, de click en el **Menú de Navegación** y posteriormente en **Infrestructura VPC**. Diríjase a la pestaña de **red** y de click en **Grupos de Seguridad**. Seleccione el grupo de seguridad que está utilizando y luego en la pestaña Reglas, habilite el puerto indicado.


## Paso 3
### Acceder al entorno gráfico 💻🏆
Un vez ha realizado la configuración el paso siguiente es acceder al entorno gráfico. Para ello, realice los siguientes pasos:

1. Abra el TightVNC Viewer en su máquina. 
2. En la sección *Connection*, en *Remote Host* colo su IP pública o flotante según sea el caso y el puerto 5901, de la siguiente manera: ```<IP>:5901```.
<p align="center"><img width="500" src="https://github.com/emeloibmco/VPC-acceso-VNC/blob/main/Imagenes/TightVNC.PNG"></p>

3. De click en **Connect**. Posteriormente le aparecerá una ventana en donde se le pide que ingrese una contraseña. En este campo ingrese la contraseña que creó el ítem 6 del [Paso 2. Habilitar el entorno gráfico de una VSI Linux](#Paso-2).
<p align="center"><img width="300" src="https://github.com/emeloibmco/VPC-acceso-VNC/blob/main/Imagenes/AccesoVNC.PNG"></p>

4. Finalmente, de click en el botón *ok* y le aparecerá el entorno gráfico de su VSI Linux, de forma similar a la siguiente imagen:
<p align="center"><img width="700" src="https://github.com/emeloibmco/VPC-acceso-VNC/blob/main/Imagenes/Ventana.PNG"></p>


## Referencias :mag:


## Autores ✒
Equipo IBM Cloud Tech Sales Colombia.
