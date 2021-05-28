# VPC-acceso-VNC 🔐
Este tutorial se enfoca en la configuración necesaria para habilitar el entorno gráfico de una VSI Linux en VPC. Es válido aclarar que esta configuración también se puede aplicar para una VSI Linux de infraestructura clásica. 

## Índice  📰
1. [Pre-Requisitos](#Pre-Requisitos-pencil)
2. [Paso 1. Datos de configuración](#Paso-1)
3. [Paso 2. Habilitar el entorno gráfico de una VSI Linux](#Paso-2)
4. [Paso 3. Acceder al entorno gráfico](#Paso-3)

## Pre-requisitos :pencil:
* Contar con una cuenta en <a href="https://cloud.ibm.com/"> IBM Cloud</a>.
* Crear una VSI linux en VPC (también puede ser en infraestructura clásica).
* En caso de contar con una VSI Linux en VCP, debe realizar de forma previa la respectiva configuración para agregar una nueva contraseña, ya que se utilizará a lo largo de este tutorial. La ruta que le permite encontrar su VSI en VPC es **Menú de Navegación → Infraestructura VPC → Instancias de Servidor Virtual.** Adicionalmente guarde la IP Flotante 
* En caso de contar con una VSI Linux en infraestructura clásica, obtenga la contraseña. Para ello, en el menú de navegación de click en Infraestructura Clásica y posteriormente en el dispositivo que va a configurar. Luego de esto, de click en la pestaña contraseñas y guarde la contraseña, ya que se utilizarán en este tutorial.

## Paso 1
### Datos de configuración ⚙
Para realizar la configuración del entorno gráfico de una VSI Linux, debe contar con los siguientes datos:
1. Contraseña:

> Nota 1: En caso de contar con una VSI Linux en VCP, debe realizar de forma previa la respectiva configuración para agregar una nueva contraseña. La ruta que le permite encontrar su VSI en VPC es Menú de Navegación → Infraestructura VPC → Instancias de Servidor Virtual.
>
> Nota 2: En caso de contar con una VSI Linux en Infraestructura Clásica, obtenga la contraseña. Para ello, en el menú de navegación de click en Infraestructura Clásica y posteriormente en el dispositivo que va a configurar. Luego de esto, de click en la pestaña contraseñas y guarde la contraseña.

2. IP:

> Nota 1: En caso de contar con una VSI Linux en VCP, la IP que se utilizará en este tutorial es la IP Flotante, la cual puede encontrar dentro de su VSI en la sección **Interfaces de red**.
>
> Nota 2: En caso de contar con una VSI Linux en Infraestructura Clásica, utilice la IP pública, la cual puede encontrar dentro de su VSI en la pestaña **Visión general** y la sección **Detalles de la red.**

## Paso 2
### Habilitar el entorno gráfico de una VSI Linux 🛠
Para habilitar el entorno gráfico de su VSI Linux, siga los pasos que se muestran a continuación:
1. Abra una ventana de *Windows PowerShell* en su máquina y establezaca una conexión vía SSH. Para ello, utilice el siguiente comando (coloque en \<IP> la IP pública o flotante según sea el caso):
``` 
ssh root@<IP> 
```
Una vez ejecute este comando se le solicitará que coloque la contraseña determinada en el [Paso 1. Datos de configuración](#Paso-1). Verifique que después de colocar la contraseña ya se encuentre dentro de la VSI, de forma similar a ``` root@nombre_vsi:~# ```

2. Posteriormente debe actualizar la lista de paquetes mediente el comando:
```
sudo apt-get update
```

3. Debe instalar el entorno de escritorio *Xface* con el comando:
```
sudo apt install xfce4 xfce4-goodies
```



## Paso 3
### Acceder al entorno gráfico 💻🏆

## Autores ✒
Equipo IBM Cloud Tech Sales Colombia.
