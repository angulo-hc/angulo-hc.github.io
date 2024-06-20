---
layout: post
title: Sistema Operativo - Desafío n°2
---

<a name="top"></a>
## Índice

- [1. Resumen del desafío](#item1)
- [2. Configuración de Servicios](#item2)
- [3. Cliente FTP](#item3)
- [4. Resolución de desafío](#item4) 
- [4. Demo](#item4)
- [5. Enlace](#item5)

<a name="item1"></a>
## 1. Resumen del desafío
Instalaremos los sistemas operativo Windows Server y windows 10, máquina cliente, en máquinas virtuales. Configuraremos la dirección IP del
servidor y configuraremos en él el rol IIS para el protocolo HTTP. En el entorno Internet Information Server (IIS) ejecutaremos configuraciones
básicas a un servidor HTTP y FTP, mediante interfaz gráfica.

**Herramientas:** Virtual Box, Windows Server, Windows 10, FileZilla.


<a name="item2"></a>
## 2. Configuración de Servicios
A continuación, configuraremos los servivios HTTP Y FTP en el servidor. Mdificaremos la página de bienvenida y activaremos el protocolo FTP.

### Configuración de la IP del servidor de una máquina virtual
Todo servidor debe tener una dirección fija, estática, que le garantice la conectividad a internet y/o para poder entregar servicios de manera 
local a la red donde está alojado. Nos estamos refiriendo a la IP local, es decir, privada. La configuración de la dirección IP del servidor en
una máquina virtual depende del sistema operativo que estemos utilizando. A continuación, veremos algunos pasos para configurar la dirección IP 
en una máquina virtual con Windows Server. Como 

**Paso 1:** Accedamos a la Configuración de Red.
* Haz clic en el menú "Inicio" y selecciona "Configuración" (icono de engranaje).
* Selecciona "Red e Internet" y luego "Configuración de red".

**Paso 2:** Accedamos a las Configuraciones de Ethernet.
* En la página de "Configuración de red", haz clic en "Cambiar opciones del
adaptador".
* Selecciona la conexión de red activa (puede llamarse "Ethernet" o
"Conexión de área local").

   ![ConfigIP_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_1.png)

**Paso 3:** Configuremos la Dirección IP.

   ![ConfigIP_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_2.png)

* Antes de introducir las configuraciones que indicaremos en las líneas que siguen,
  si no conocemos la información solicitada, hacemos clic en "Detalles" en la imagen de
  arriba y nos conducirá a

  ![ConfigIP_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_3.png)

  donde obtendremos toda la información que se nos solicitará.

* De vuelta a la primera imagen del Paso 3, haz clic en "Propiedades" y tendrás algo
  como la siguiente ilustración:
  
    ![ConfigIP_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_4.png)  

* Selecciona "Protocolo de Internet versión 4 (TCP/IPv4)" y haz doble clic. 

   ![ConfigIP_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_5.png) 

* Selecciona "Usar la siguiente dirección IP".
   Ingresa la dirección IP deseada en el campo "Dirección IP". Por
ejemplo, "192.168.1.2".
* Ingresa la máscara de subred en el campo correspondiente. Por
ejemplo, "255.255.255.0". Recordemos que siempre debe estar configurada la mascara
para que nuestra máquina virtual reconozca en la red que está y de esta manera logre comunicarse
 con los demás dispositivos de nuestra LAN.
* Ingresa la puerta de enlace predeterminada en el campo "Puerta de
enlace". Puede ser la dirección IP del router en tu red.
* Ingresa las direcciones de servidor DNS si es necesario.

  ![ConfigIP_6]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_6.png) 
   
**Paso 4:** Apliquemos los Cambios.
* Haz clic en "Aceptar" para cerrar las ventanas de propiedades.

**Paso 5:** Verifica la Configuración.
* Para verificar la configuración, puedes abrir una ventana de símbolo del
sistema y ejecutar el comando `ipconfig`. Asegúrate de que la dirección IP,
la máscara de subred y la puerta de enlace se muestren correctamente.

  ![ConfigIP_7]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigIP_7.png) 

### Configuración de rol IIS, protocolos HTTP y FTP
El rol en Windows Server permite que el servidor actúe como un servidor web (A vecees
también llamados servidor HTTP). Cuando configuramos el protocolo HTTP en IIS,
básicamente estamos diciendo *"Vamos a utilizar este camino especial (protocolo) para
que los clientes puedan solicitar y recibir páginas web"*. Por otro lado, tenemos que
FTP es un servicio que tiene conexión directa al servicio HTTP. No sólo funciona para
páginas web, funciona para otro tipo de servidores como, por ejemplo, servidores de
almacenamiento de archivos. FTP nos permite eliminar, editar, subir archivos, de manera
remota, desde una computadora cliente, al servidor HTTP.


**Paso 1:** Acceder al Administrador del Servidor.
* Presiona la tecla `Windows` y selecciona "Administrador del Servidor".

  ![ConfigRol_IIS_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_1.png)

**Paso 2:** Agrega el Rol IIS.
* En el Administrador del Servidor, selecciona "Agregar roles y
características".

   ![ConfigRol_IIS_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_2.png)

* En el asistente para agregar roles, selecciona "Servicios de Rol" y elige
"Servidor web (IIS)".

   ![ConfigRol_IIS_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_3.png)

* Marca la opción "Servidor FTP" dentro de "Servicios de rol adicionales
para Servidor web (IIS)".

  ![ConfigRol_IIS_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_4.png)
  
* Haz clic en "Siguiente" y luego en "Instalar". Sigue los pasos para
completar la instalación del rol IIS con el servicio FTP.

  ![ConfigRol_IIS_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_5.png)

  ![ConfigRol_IIS_6]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_6.png)

**Paso 3:** Configura el Sitio Web
* Una vez instalado IIS con el servicio FTP, abre el "Administrador de IIS".

   ![ConfigRol_IIS_7]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_7.png)
  
* En el Administrador de IIS, selecciona el nodo del servidor. Para identificar
  el nodo del servidor, lo podemos hacer desde la terminal, ejecutando el comando
   `hostname`.

    ![ConfigRol_IIS_8]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_8.png)

* Haz clic en "Agregar sitio" en el panel derecho.
* Completa los detalles del sitio, incluyendo el nombre, la ruta física del
  contenido del sitio y la configuración del puerto (por ejemplo, el puerto 80
  para HTTP).
* Haz clic en "Aceptar" para crear el sitio.

**Paso 4:** Configura el sitio FTP
* Seleccione algún *sitio* creado a partir del paso anterior. Para ilustrar este
   paso, seleccionaremos el sitio web que existe por defecto.
* Haz clic derecho es el sitio web en "Agregar sitio FTP" en el panel derecho.

   ![ConfigRol_IIS_91]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_91.png)

* Completa los detalles del sitio FTP, incluyendo el nombre, la ruta física del
  contenido y la configuración del puerto (por ejemplo, el puerto 21 para
  FTP).

   ![ConfigRol_IIS_10]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_10.png)
  
* Configura la autenticación y el control de acceso según tus necesidades.
  Puedes elegir autenticación básica o anónima, y configurar usuarios y
  permisos de acceso.

   ![ConfigRol_IIS_11]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_11.png)
  
* Haz clic en "Siguiente" y luego en "Finalizar".

   ![ConfigRol_IIS_12]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_12.png)
  
<a name="index"></a>
**Paso 5:** Verifica la Configuración de sitio web
* Abre un navegador web y accede al sitio utilizando la dirección IP del
  servidor o el nombre del servidor. Por ejemplo, `http://localhost` o
  `http://<dirección_ip_del_servidor>`.

    ![ConfigRol_IIS_13]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ConfigRol_IIS_13.png)

La diferencia *sitio web* y *sitio FTP* es que el *sitio web* es una página de una aplicación que se 
alojará dentro del servidor mientras que el *sitio FTP* es la ubicación física, dentro del servidor,
donde se alojan los archivos o aplicaciones web.

El directorio físico de estos archivos de las aplicaciones web se encuentra en la raiz `C:\inetpub\wwwroot`.
Este directorio sólo existirá luego de instalar el rol IIS. Si tenemos múltples *sitios web* alojados
en el servidor, por cada uno de estos tendremos una carpeta siteada en la raiz del directorio que
acabamos de mencionar.

Cuando administramos más de un sitio web dentro de una plataforma IIS, no tiene sentido darle adminitración
FTP a cada sitio individualmente si FTP usará el mismo puerto 21 porque sólo se podrá ingresar, por
defecto desde una máquina cliente, al primer sitio que se hizo la configuración. Para administrar FTP
en estos casos, lo que debemos hacer es agregar en *sitios* (Ver imagen del Paso 4) un sitio FTP el
cual tenga acceso a una carpeta que contenga a todas las carpetas que alojarán los distisntos sitios
web.



<a name="item3"></a>
## 3. Cliente FTP
Para la utilización de FTP, desde un *cliente remoto*, existen distintas opciones de
software que nos permitirán poder hacerlo. Entre alguno de ellos tenemos:

**FileZilla**
- Plataformas: Windows, Linux, macOS.
- Descripción: FileZilla es un cliente FTP de código abierto muy popular. Es fácil
de usar y soporta FTP sobre TLS/SSL (FTPS) y SSH File Transfer Protocol (SFTP).

**WinSCP**
- Plataforma: Windows.
- Descripción: WinSCP es un cliente SFTP y SCP gratuito para Windows. Además de
  la interfaz gráfica, también ofrece una interfaz de línea de comandos.

**Cyberduck**
- Plataforma: Windows, macOS.
- Descripción: Cyberduck es un cliente FTP de código abierto que también admite
  otros protocolos como SFTP, WebDAV y Amazon S3. Tiene una interfaz de usuario
  intuitiva.

**Command-line FTP** (incluido en sistemas operativos)
- Plataforma: Windows, Linux, macOS.
- Descripción: Los sistemas operativos como Windows, Linux y macOS a menudo
  incluyen un cliente FTP de línea de comandos. En Windows, por ejemplo,
  puedes usar el comando ftp desde el símbolo del sistema.

  Todos los Sistemas Operativos cuentan con las herramientas FTP embebida en sus
  consolas o líneas de comando. En el caso del rol IIS en servidores, HTTP viene
  inmerso dentro de él, por lo que no hay que hacer configuración adicional para
  activarlo.

  A continuación, instalaremos un cliente FTP en la máquina virtual de cliente, para realizar 
  pruebas de transferencia de archivos.

**Paso 1:** Verificar la Configuración.
* Descarga FileZilla desde el sitio oficial: https://filezilla-project.org/
  Instala FileZilla en tu máquina local.

  ![ClienteFTP_1.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_1.png)

**Paso 2:** Abre FileZilla
* Abre FileZilla en tu máquina local.
![ClienteFTP_21.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_21.png)

**Paso 3:** Configura la Conexión al Servidor FTP
* En FileZilla, ve al menú "Archivo" y selecciona "Gestor de sitios"
  
  ![ClienteFTP_3.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_3.png)
    
* Haz clic en "Nuevo sitio" y asigna un nombre descriptivo al servidor FTP.

  ![ClienteFTP_4.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_4.png)

* Ingresa la dirección IP o el nombre del servidor en el campo "Servidor".
* Establece el protocolo a "FTP" y el tipo de inicio de sesión a "Normal".
* Ingresa el nombre de usuario y la contraseña proporcionados durante la
  configuración del servidor FTP.
  
  ![ClienteFTP_5.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_5.png)
  
* Haz clic en "Conectar" para guardar la configuración.

**Paso 4:** Transfiere Archivos desde el Cliente
* En la ventana principal de FileZilla, verás dos paneles. El de la izquierda
  muestra los archivos locales, y el de la derecha muestra los archivos
  remotos en el servidor FTP.

  ![ClienteFTP_6.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_6.png)
  
* Navega a la ubicación de los archivos locales que deseas transferir en el
panel izquierdo.
* Selecciona los archivos y/o carpetas que deseas transferir.
* Arrastra y suelta los archivos en el panel derecho para iniciar la
transferencia.

 ![ClienteFTP_7.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_7.png)
  
**Paso 5:** Descarga Archivos hacia el Cliente
* Para descargar archivos desde el servidor FTP a tu máquina local,
  selecciona los archivos en el panel derecho.
* Arrastra y suelta los archivos en el panel izquierdo para iniciar la
  descarga.

**Paso 6:** Verifica la Transferencia
 * En la parte inferior de la ventana de FileZilla, podrás ver el progreso de la
   transferencia. Asegúrate de que los archivos se transfieran correctamente
   sin errores.
 * En el directorio del servidor en donde se agregaron los archivos desde el cliente FTP,
   debería registrarse los cambios

  ![ClienteFTP_8.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_8.png)
   
 * Para la iustración de este ejemplo, se modificó el [index.html](#index) de bienvenida que venía por
   defecto e iustramos.

  ![ClienteFTP_91.png]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_2/ClienteFTP_91.png)
   
<a name="item4"></a>
## 4. Demo
A continuación, encontrará un video ilustrativo de cómo se ejecuta la aplicación cuando se decide jugar una partida.

<a name="item5"></a>
## 5. Enlaces
* [Windows Server](https://www.microsoft.com/es-es/evalcenter/download-windows-server-2019)
* [Windows 10](https://www.microsoft.com/es-es/software-download/windows10)
* [FileZilla](https://filezilla-project.org/)


[Volver a índice](#top)
