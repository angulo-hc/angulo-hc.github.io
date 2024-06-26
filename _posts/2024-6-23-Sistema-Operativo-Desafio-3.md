---
layout: post
title: Sistema Operativo - Desafío n°3
---
Se plicarán objetos de *Active Directory¨* para resolver un problema planteado en un entorno de Windows Server. El objetivo es utilizar los objetos de *AD* de manera
efectiva para implementar políticas de roles comunes y abordar un escenario específico. La
actividad se centrará en la creación y gestión de usuarios, grupos y políticas de grupo (*GPO*).

<a name="top"></a>
## Índice

- [1. Consigna del desafío](#item1)
- [2. Configuración de los escenarios](#item2)
- [3.Unidades organizativas, usuario y grupos de seguridad en Active Directory](#item3)
- [4. Políticas de Grupo (GPOs)](#item4)
- [5. Permisos de Acceso a Recursos](#item5)
- [6. Demo](#item6)
- [7. Enlaces](#item7)
  

<a name="item1"></a>
## 1. Consigna del desafío #############

### Escenario Prueba

**Empresa:** TechSolutions Inc.

**Sector:** Desarrollo de software y servicios tecnológicos.

**Escenario:** TechSolutions Inc. está creciendo rápidamente y ha contratado a nuevos empleados en varios departamentos, incluidos Desarrollo,
Recursos Humanos (RRHH), y Ventas. La empresa necesita asegurar que los datos y recursos sensibles sean accesibles solo para aquellos que lo
necesiten, así como aplicar configuraciones específicas en los equipos de los usuarios según sus roles y departamentos.

### Requerimientos

**1. Restringir acceso a ciertos recursos**
* Solo los empleados del departamento de RRHH deben tener acceso a los archivos de nómina.
* Solo los desarrolladores deben tener acceso a los servidores de desarrollo y herramientas de programación específicas.
* El equipo de Ventas necesita acceso exclusivo a la base de datos de clientes y herramientas de gestión de relaciones con clientes (CRM).

**2. Aplicar configuraciones específicas en los equipos de los usuarios** 
* Todos los empleados deben tener una política de contraseñas fuerte y un bloqueo de pantalla automático tras 10 minutos de inactividad.
  Los desarrolladores necesitan tener configuraciones específicas para entornos de desarrollo (por ejemplo, instalar software como *Visual
  Studio*.
* Los empleados de Ventas necesitan tener configuraciones específicas para acceso rápido a las aplicaciones CRM y a los correos electrónicos.
* El equipo de RRHH necesita tener configuraciones específicas para herramientas de gestión de personal y software de nómina.
Implementación de políticas de roles comunes en Windows Server.

**3. Crear Grupos de Seguridad en Active Directory**
* Grupo: Desarrollo
* Grupo: RRHH
* Grupo: Ventas
* Grupo: Todos los Empleados

**4. Configurar Políticas de Grupo (GPOs)**

* GPO para Contraseñas y Bloqueo de Pantalla:
  * Aplicar una política de contraseñas fuertes (mínimo de 12 caracteres, inclusión de números y caracteres especiales).
  * Configurar el bloqueo de pantalla automático tras 10 minutos de inactividad.
  * Enlazar esta GPO al contenedor de Todos los Empleados.
    
* GPO para el Departamento de Desarrollo:
  * Instalar automáticamente software de desarrollo como Visual Studio.
  * Enlazar esta GPO al contenedor del grupo Desarrollo.
    
* GPO para el Departamento de Ventas:
  * Configurar acceso directo a aplicaciones CRM y correo electrónico.
  * Enlazar esta GPO al contenedor del grupo Ventas.
    
* GPO para el Departamento de RRHH:
  * Instalar software de gestión de personal y nómina.
  * Configurar acceso exclusivo a los archivos de nómina mediante permisos de archivo.
  * Enlazar esta GPO al contenedor del grupo RRHH.
    
**5. Configurar Permisos de Acceso a Recursos:**
* Carpeta Nómina:
  * Solo el grupo RRHH tiene permisos de lectura y escritura.
* Servidores de Desarrollo:
  * Solo el grupo Desarrollo tiene permisos de acceso.
* Base de Datos de Clientes:
  * Solo el grupo Ventas tiene permisos de lectura y escritura.

<a name="item2"></a>
## 2. Configuración de los escenarios #############

### Configuraciones básicas del Servidor - Configuración de la IP

Todo servidor debe tener una dirección fija, estática, que le garantice la conectividad a internet y/o para poder entregar servicios
de manera local a la red donde está alojado. Nos estamos refiriendo a la IP local, es decir, privada.

**Paso 1:** Accedamos a la Configuración de Red.
* Haz clic en el menú "Inicio" y selecciona "Configuración" (icono de engranaje).
* Selecciona "Red e Internet" y luego "Configuración de red".

**Paso 2:** Accedamos a las Configuraciones de Ethernet.
* En la página de "Configuración de red", haz clic en "Cambiar opciones del adaptador".
* Selecciona la conexión de red activa (puede llamarse "Ethernet" o "Conexión de área local").

**Paso 3:** Configuremos la Dirección IP.
* Haz clic en "Detalles", donde obtendremos toda la información que se nos solicitará.
* Haz clic en "Propiedades" Y selecciona "Protocolo de Internet versión 4 (TCP/IPv4)" y haz doble clic. 
* Selecciona "Usar la siguiente dirección IP".
* Ingresa la dirección IP deseada en el campo "Dirección IP". Por ejemplo, "192.168.1.2".
* Ingresa la máscara de subred en el campo correspondiente. Por ejemplo, "255.255.255.0". Recordemos que siempre debe estar configurada la
  mascara para que nuestra máquina virtual reconozca en la red que está y de esta manera logre comunicarse con los demás dispositivos de
  nuestra LAN.
* Ingresa la puerta de enlace predeterminada en el campo "Puerta de enlace". Puede ser la dirección IP del router en tu red.
* Ingresa las direcciones de servidor DNS si es necesario.

  ![Configuracion_IP]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/Configuracion_IP.png) 

### Configuraciones de Roles Primarios - Rol Active Directory

**Paso 1:** Accede al Administrador del Servidor
* Presiona Win + X y selecciona "Administrador del Servidor".

**Paso 2:** Agrega el Rol de Servicios de Dominio de Active Directory
* En el Administrador del Servidor, selecciona "Agregar roles y características".

  ![ConfiguracionAD_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_1.png) 
  
* En el asistente para agregar roles, selecciona "Servicios de Rol" y elige "Servicios de Dominio de Active Directory".

  ![ConfiguracionAD_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_2.png) 
  
* Haz clic en "Siguiente" y luego en "Instalar". Sigue los pasos para completar la instalación del rol.

### Configuraciones de Dominio de Active Directory

**Paso 1:** Configura AD DS
* Después de instalar el rol, aparecerá una notificación. Haz clic en "Promocionar este servidor a controlador de dominio".

  ![ConfiguracionAD_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_3.png) 
  
* Selecciona la opción "Agregar un nuevo bosque" y proporciona el nombre de dominio deseado (por ejemplo, midominio.local).

  ![ConfiguracionAD_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_4.png)
  
* Establece una contraseña para la base de datos de AD DS y haz clic en "Siguiente".

  ![ConfiguracionAD_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_5.png) 

* En la página "Funcionalidad del bosque", elige el nivel de funcionalidad adecuado para tus necesidades y haz clic en 
  "Siguiente".

  ![ConfiguracionAD_6]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_6.png)
  
* En la página "Ubicación de archivos de base de datos", elige la ubicación de los archivos de base de datos de AD DS y haz 
  clic en "Siguiente".
* Revisa la configuración en la página de resumen y haz clic en "Siguiente" para iniciar la instalación.

**Paso 2:** Configura DNS
* Si aún no tienes el rol de Servidor DNS instalado, el asistente te pedirá instalarlo. Acepta la instalación automática.
* Configura DNS según tus preferencias y haz clic en "Siguiente".

**Paso 3:** Configura la Contraseña de Modo de Restauración de Servicio (DSRM)
* Configura la contraseña de modo de restauración de servicio (DSRM) y haz clic en "Siguiente".
* Revisa la configuración en la página de resumen y haz clic en "Siguiente" para iniciar la instalación.

**Paso 4:** Completa la Instalación
* Después de la instalación, el servidor se reiniciará automáticamente.

**Paso 5:** Verifica el Dominio
* Después del reinicio, inicia sesión con las credenciales del nuevo dominio.

  ![ConfiguracionAD_7]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_7.png)

  ![ConfiguracionAD_8]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionAD_8.png)
  
### Configuraciones en dispositivos Clientes

**Paso 1:** Configuración de IP del Servidor DNS
* "Administrador de Active Directory" en tu máquina virtual.

    ![ConfiguracionDNS_Cliente]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionDNS_Cliente.png)

**Paso 2:** Configuración del Dominio
* Desde el panel izquierdo, en "Este Equipo", hacer clic derecho y doble clic en "Propiedades"

    ![ConfigDeDominioEnCliente_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_1.png)

* En lo que sigue, siga los pasos como lo ilustran las imágenes

    ![ConfigDeDominioEnCliente_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_2.png)

    ![ConfigDeDominioEnCliente_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_3.png)

    ![ConfigDeDominioEnCliente_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_4.png)

    ![ConfigDeDominioEnCliente_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_5.png)

* Una vez configurado el dominio, si el procedimiento ha sido exitoso, deberíamos visibilizar información como la
  de las siguientes imágenes

    ![ConfigDeDominioEnCliente_6]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_6.png)

    ![ConfigDeDominioEnCliente_7]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_7.png)

* Al restaurar el equipo cliente, en la interfaz de inicio de sesión deberá tener algo como:

    ![ConfigDeDominioEnCliente_8]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfigDeDominioEnCliente_8.png)


<a name="item3"></a>
## 3. Unidades organizativas, usuario y grupos de seguridad en Active Directory

### Creación de Unidades Organizativas
A continuación, de acuerto a la especificación de nuestro escenario, proseguiremos a crear tres unidades organizativas, 
dentro de del domino *techsolutions*Ñ Ventas, Desarrolladores, RRHH.

**Paso 1:** Accede al Administrador de Active Directory
* "Administrador de Active Directory" en tu máquina virtual.

    ![ConfiguracionUO_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionUO_1.png)

**Paso 2:** Crear Unidades Organizativas (UO)
* En el panel izquierdo, selecciona el nombre de tu dominio en la estructura del árbol.

    ![ConfiguracionUO_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionUO_2.png)

* Haz clic derecho y elige "Nueva" -> "Unidad Organizativa".

    ![ConfiguracionUO_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionUO_3.png)
  
* Por cada departamento, *RRHH*, *Desarrolladores*, *Ventas*, descrito en *escenario* de desafío, asigna una *UO*.

    ![ConfiguracionUO_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionUO_4.png)

    ![ConfiguracionUO_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/ConfiguracionUO_5.png)

### Creación de usuarios y grupos de seguridad

**Paso 1:** Crear usuarios
* Dentro de cada *UO*, crea usuarios según la estructura organizativa. Haz clic derecho en la UO, 
  selecciona "Nuevo" y elige Usuario.

    ![CreacionUsuario_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_1.png) 

* Ingresa la información necesaria para cada usuario, como nombre, contraseña, etc.

    ![CreacionUsuario_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_2.png)

  ![CreacionUsuario_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_3.png)

**Paso 2:** Crear grupos
* Dentro de cada *UO*, crea un *grupo* según la estructura organizativa.

    ![CreacionGrupos_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionGrupos_1.png)

* Ingresa la información necesaria para cada grupo

    ![CreacionGrupos_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionGrupos_2.png)

* Una vez creado los grupos, por cada Unidad Organizativa, agregar los usuarios a estos haciendo 
  doble clic en estos objetos
  
    ![UsuariosEnGrupos_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/UsuariosEnGrupos_1.png)

    ![UsuariosEnGrupos_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/UsuariosEnGrupos_2.png)

    ![UsuariosEnGrupos_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/UsuariosEnGrupos_3.png)

    ![UsuariosEnGrupos_4]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/UsuariosEnGrupos_4.png)

    ![UsuariosEnGrupos_5]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/UsuariosEnGrupos_5.png)


<a name="item4"></a>
## 4. Políticas de Grupo (GPOs)

A continuación, asignaremos las GPO a configuraciones específicas de acuerdo a los requerimientos dados


### Interfaz de configuración

**Paso 1:** Posicionarnos en la interfaz en donde editaremos las GPO requeridas
* Desde nuestro Servidor, haciendo clic en Windows, escribimos "Gestión de Políticas de Grupo". 

    IMAGEN

* Haciendo doble clic en "Gestión de Políticas de Grupo" y clic en el dominio "techsolutions" que se nos
   muestra en el panel izquierdo, estaremos posicionados en el área donde crearemos nuestras GPO

    IMAGEN

    Notemos en esta última imagen que tendremos desplegadas carpetas con el mismo nombre de cada Unidad
    Organizativa que hemos creado en el Paso 3.

### GPO para Contraseñas y Bloqueo de Pantalla

**Paso 1:** GPO para Contraseñas
* Las GPO para este requerimiento será aplicada para todos los usuarios de nuestra organización por lo que,
  directamente desde nuestro dominio techsolutions.local, haciendo clic derecho, luego clic en "Crear una GPO
  en este Dominio", se crea la politica con nombre "password"

    IMAGEN 4

* A continuación, una vez creada la GPO *"password"*, hacemos clic derecho en esta, desde el panel izquierdo y
  luego clic en la opción Editar

   IMAGEN 5

* En esta última interfaz que se despliega tendremos todos los parámetros que existen para poder agregar politícas,
  restricciones, etc.

   IMAGEN 6

   Veemos que tenemos configuraciones a nivel de computadora y a nivel de usuarios.


**Paso 2:** GPO para Bloqueo de Pantalla  
* Configurar el Tiempo de Inactividad. En el Editor de Administración de Políticas de Grupo, navega hasta
    
    > Configuración de usuario > Plantillas administrativas > Panel de control > Personalización
      
* En el panel derecho, busca y haz doble clic en la política denominada "Esperar tiempo antes de activarse el protector
     de pantalla".       

  IMAGEN 10

* Selecciona "Habilitada" y luego en el cuadro "Segundos" introduce el valor correspondiente a 10 minutos (600 segundos).
    Haz clic en "Aplicar", luego "Aceptar".

  IMAGEN 11

**Paso 2:** Habilitar el Protector de Pantalla
* En la misma ruta del paso anterior, busca y haz doble clic en la política "Habilitar protector de pantalla".

  IMAGEN 12

* Selecciona "Habilitada" y haz clic en "Aplicar", luego "Aceptar".

  IMAGEN 13
  
**Paso 3** Proteger con Contraseña el Protector de Pantalla  
    
* En la misma ruta del paso 1, busca y haz doble clic en la política "Protector de pantalla: proteger con contraseña".
  Selecciona "Habilitada" haz clic en "Aplicar", luego "Aceptar".    

## GPO para el Departamento de Desarrollo

**GPO para la instalación automática de desarrollo: Visual Studio Code**

**Paso 1:** Obtener el archivo .msi de Visual Studio Code
  1. Ve al sitio oficial de Visual Studio Code y descarga el archivo .exe de la versión que deseas instalar.

       [Visual Studio Code .exe Download](https://code.visualstudio.com/download)

  2. Desde Microsoft Store   
       


Para automatizar la instalación de Visual Studio Code en las computadoras clientes desde un servidor Active Directory,
puedes usar la Política de Grupo (Group Policy) junto con un archivo MSI de Visual Studio Code.

**Paso 1:** Preparativos
* Se descarga el instalador de Visual Studio desde el sitio oficial y guárdalo en una carpeta compartida accesible por todos
  los equipos en la red. Este instalador debe ser el archivo .msi o .exe.

* Se crea una carpeta compartida en el servidor donde almacenarás los archivos de instalación. Asegúrate de que todos los equipos
   que recibirán la instalación tengan permisos de lectura en esta carpeta.  
  
**Paso 2:** Configuración de la GPO

* Abrir la Consola de Administración de Políticas de Grupo (GPMC). Una opción es hacerlo escribiendo "gpmc.msc" en el
 cuadro de búsqueda o en el menú de inicio y presionar Enter.
* Crear una Nueva GPO, de la misma forma que hemos hecho en pasos de secciones anteriores. En este caso, nombraremos a
  esta GPO "Instalación de Visual Studio Code". Esta GPO será creada desde la carpeta "Desarrolladores".


## Grupos de Seguridad en Active Directory
  
## Configurar Políticas de Grupo (GPOs)

## Configuración de permisos de Acceso a recursos


  

<a name="item4"></a>
## 4. Demo

    
