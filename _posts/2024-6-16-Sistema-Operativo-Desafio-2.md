---
layout: post
title: Sistema Operativo - Desafío n°2
---

<a name="top"></a>

## Índice

- [1. Resumen del desafío](#item1)
- [2. Configuración de Servicios](#item2)
- [3. Cliente FTP](#item3)
- [4. Demo](#item4)
- [5. Enlace](#item5)
- [6. Herramientas](#item6) 

<a name="item1"></a>
### 1. Resumen del desafío
Instalaremos los sistemas operativo Windows Server y windows 10, máquina cliente, en máquinas virtuales. Configuraremos la dirección IP del
servidor y configuraremos en él el rol IIS para el protocolo HTTP. En el entorno Internet Information Server (IIS) ejecutaremos configuraciones
básicas a un servidor HTTP y FTP, mediante interfaz gráfica.

**Herramientas:** Virtual Box, Windows Server, Windows 10, FileZilla.


<a name="item2"></a>
### 2. Configuración de Servicios
A continuación, configuraremos los servivios HTTP Y FTP en el servidor. Mdificaremos la página de bienvenida y activaremos el protocolo FTP.

#### Configuración de la IP del servidor de una máquina virtual
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

#### Configuración de rol IIS, protocolos HTTP y FTP
El rol en Windows Server permite que el servidor actúe como un servidor web (A vecees
también llamados servidor HTTP). Cuando configuramos el protocolo HTTP en IIS,
básicamente estamos diciendo *"Vamos a utilizar este camino especial (protocolo) para
que los clientes puedan solicitar y recibir páginas web"*. Por otro lado, tenemos que
FTP es un servicio que tiene conexión directa al servicio HTTP. No sólo funciona para
páginas web, funciona para otro tipo de servidores como, por ejemplo, servidores de
almacenamiento de archivos. FTP nos permite eliminar, editar, subir archivos, de manera
remota, desde una computadora cliente, al servidor HTTP.


**Paso 1:** Acceder al Administrador del Servidor.
* Presiona la tecla `Win` y selecciona "Administrador del Servidor".

**Paso 2:** Agrega el Rol IIS.
* En el Administrador del Servidor, selecciona "Agregar roles y
características".
* En el asistente para agregar roles, selecciona "Servicios de Rol" y elige
"Servidor web (IIS)".
* Marca la opción "Servidor FTP" dentro de "Servicios de rol adicionales
para Servidor web (IIS)".
* Haz clic en "Siguiente" y luego en "Instalar". Sigue los pasos para
completar la instalación del rol IIS con el servicio FTP.

**Paso 3:** Configura el Sitio FTP.
* Una vez instalado IIS con el servicio FTP, abre el "Administrador de IIS".
  selecciona el nodo del servidor. Para identificar el nodo del servidor, lo
  podemos hacer desde la terminal, ejecutando el comando `hostname`.
* Haz clic en "Agregar sitio FTP" en el panel derecho.
* Completa los detalles del sitio FTP, incluyendo el nombre, la ruta física del
  contenido y la configuración del puerto (por ejemplo, el puerto 21 para
  FTP).
* Configura la autenticación y el control de acceso según tus necesidades.
  Puedes elegir autenticación básica o anónima, y configurar usuarios y
  permisos de acceso.
* Haz clic en "Siguiente" y luego en "Finalizar".

**Paso 5:** Verificar la Configuración.
 * Descarga FileZilla desde el sitio oficial: https://filezilla-project.org/
 * Instala FileZilla en tu máquina local.
* Abre un cliente FTP (por ejemplo, FileZilla) en una máquina remota y
  conecta al servidor FTP utilizando la dirección IP o nombre del servidor y
  el puerto configurado.
  

<a name="item3"></a>
### 3. Cliente FTP
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

**Paso 2:** Abre FileZilla
* Abre FileZilla en tu máquina local.

**Paso 3:** Configura la Conexión al Servidor FTP.
* En FileZilla, ve al menú "Archivo" y selecciona "Gestor de sitios"..
* Haz clic en "Nuevo sitio" y asigna un nombre descriptivo al servidor FTP.
* Ingresa la dirección IP o el nombre del servidor en el campo "Servidor".
* Establece el protocolo a "FTP" y el tipo de inicio de sesión a "Normal".
* Ingresa el nombre de usuario y la contraseña proporcionados durante la
  configuración del servidor FTP.
* Haz clic en "Conectar" para guardar la configuración.

**Paso 4:** Transfiere Archivos desde el Cliente
* En la ventana principal de FileZilla, verás dos paneles. El de la izquierda
  muestra los archivos locales, y el de la derecha muestra los archivos
  remotos en el servidor FTP.
* Navega a la ubicación de los archivos locales que deseas transferir en el
panel izquierdo.
* Selecciona los archivos y/o carpetas que deseas transferir.
* Arrastra y suelta los archivos en el panel derecho para iniciar la
transferencia.

**Paso 5:** Descarga Archivos hacia el Cliente
* Para descargar archivos desde el servidor FTP a tu máquina local,
  selecciona los archivos en el panel derecho.
* Arrastra y suelta los archivos en el panel izquierdo para iniciar la
  descarga.

**Paso 6:** Verifica la Transferencia
 * En la parte inferior de la ventana de FileZilla, podrás ver el progreso de la
   transferencia. Asegúrate de que los archivos se transfieran correctamente
   sin errores.




* Solución: Crear un display de bienvenida con un botón que permita acceder al juego.

* Criterio mínimo de aceptación: Al hacer click en el botón _"Jugar"_, se produzca el display del juego.

Product Backlog
- Incorporar display de bienvenida y botones que guiarán al usuario en el juego.
- Dar funcionalidad al botón para que lleve al usuario al display de juego.
- Hacer una App _responsive_.


**HU 2. "Como jugador quiero que tenga detalles relacionados con Pokémon, para poder encontrarlo coherente con mi búsqueda".**

_CARACTERÍSTICAS: El usuario debe encontrar coherencia en el diseño de la aplicación y la tematica Pokémon ._

* Solución: Crear un diseño acorde a los colores, elementos (ventanas de diálogo, pokeball, imágenes de pokemones, entre otras), y tipografía de pokémon.
* Criterio mínimo de aceptación: Al visualizar la página se entienda el contexto de pokémon.

Product Backlog
- buscar fuentes creadoras de tipografia de pokémon. 
- crear un nombre de la aplicación que se relacione con la temática de pokémon.
- crear interfaz con colores de pokémon
- incorporar elemento de diseño distintivo de pokémon en la cara frontal de las cartas.
- crear mensaje emergente que se visualice como ventana de diálogo.


**HU 3. "Como jugador quiero que sea de acceso rápido y sencillo, para poder disfrutar del juego lo más que sea posible en mi tiempo libre."**

_CARACTERÍSTICAS: El usuario debe poder acceder rápido al juego, y que este sea intuitivo ._
* Solución: crear una interfaz sencilla, sin tanto texto y con botones que guien al usuario en la funcionalidad del juego.
* Criterio mínimo de aceptación: Deben existir dos botones, uno que nos lleve al display del juego, y otro que nos lleve al display de instrucciones.

Product Backlog
- crear botones con funcionalidad (juego, instrucciones, entre otras), para que el usuario pueda utilizarlos cuando requiere la información.

<a name="item4"></a>
### 4. Demo
A continuación, encontrará un video ilustrativo de cómo se ejecuta la aplicación cuando se decide jugar una partida.

https://github.com/Hilicarolina/SCL017-memory-match-game/assets/14808063/abe2bad1-13f9-426b-8f45-743362493d3a


<a name="item5"></a>
### 5. Enlace
https://hc-angulo.github.io/memory-match-game/src 

[Volver a índice](#top)

<a name="item6"></a>
### 6. Herramientas
<p align="left>
 <a href="" target="_blank">
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/html5/html5-original.svg" alt="html5" width="50" height="50"/>
<a href="" target="_blank">            
            <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/css3/css3-original.svg" alt="css3" width="50" height="50"/></a>
           </a>
 <a href="" target="_blank">      
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/javascript/javascript-original.svg" alt="javascript" width="50" height="50"/></a>
 </p>
