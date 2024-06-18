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
Instalaremos los sistemas operativo Windows Server y windows 10, máquina cliente, en máquinas virtuales. Configuraremos la dirección IP del servidor y configuraremos en él el rol IIS para el protocolo HTTP. 
En el entorno Internet Information Server (IIS) ejecutaremos configuraciones básicas a un servidor HTTP y FTP, mediante interfaz gráfica

**Herramientas:** Virtual Box, Windows Server, Windows 10, FileZilla.


<a name="item2"></a>
### 2. Configuración de Servicios
A continuación, configuraremos los servivios HTTP Y FTP en el servidor. Mdificaremos la página de bienvenida y activaremos el protocolo FTP.

#### Configuración de la IP del servidor de una máquina virtual
Todo servidor debe tener una dirección fija, estática, que le garantice la conectividad a internet y/o para poder entregar servicios de manera local a la red donde está alojado. Nos estamos refiriendo a la IP local, es decir, privada. La configuración de la dirección IP del servidor en una máquina virtual depende del sistema operativo que estemos utilizando. A continuación, veremos algunos pasos para configurar la dirección IP en una máquina virtual con Windows Server. Como 

**Paso 1:** Accedamos a la Configuración de Red.
* Haz clic en el menú "Inicio" y selecciona "Configuración" (icono de engranaje).
* Selecciona "Red e Internet" y luego "Configuración de red".

**Paso 2:** Accedamos a las Configuraciones de Ethernet.
* En la página de "Configuración de red", haz clic en "Cambiar opciones del
adaptador".
* Selecciona la conexión de red activa (puede llamarse "Ethernet" o
"Conexión de área local").

**Paso 3:** Configuremos la Dirección IP.
* En las propiedades de la conexión, busca y selecciona "Protocolo de
Internet versión 4 (TCP/IPv4)" y haz clic en "Propiedades".
* Selecciona "Usar la siguiente dirección IP".
   Ingresa la dirección IP deseada en el campo "Dirección IP". Por
ejemplo, "192.168.1.2".
* Ingresa la máscara de subred en el campo correspondiente. Por
ejemplo, "255.255.255.0". Recordemos que siempre debe estar configurada la mascara
para que nuestra máquina virtual reconozca en la red que está y de esta manera logre comunicarse con los demás dispositivos de nuestra LAN.
* Ingresa la puerta de enlace predeterminada en el campo "Puerta de
enlace". Puede ser la dirección IP del router en tu red.
* Ingresa las direcciones de servidor DNS si es necesario.

**Paso 4:** Apliquemos los Cambios.
* Haz clic en "Aceptar" para cerrar las ventanas de propiedades.

**Paso 5:** Verifica la Configuración.
* Para verificar la configuración, puedes abrir una ventana de símbolo del
sistema y ejecutar el comando `ipconfig`. Asegúrate de que la dirección IP,
la máscara de subred y la puerta de enlace se muestren correctamente.




<a name="item3"></a>
### 3. Cliente FTP
Instalaremos un cliente FTP en la máquina virtual de cliente, para realizar pruebas de transferencia de archivos.





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
