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
- [2. Configuración de Servicios](#item2)
- [3. Cliente FTP](#item3)
- [4. Demo](#item4)
- [5. Enlace](#item5)




### Configuración de la IP del servidor de una máquina virtual
Todo servidor debe tener una dirección fija, estática, que le garantice la conectividad a internet y/o para poder entregar servicios de manera 
local a la red donde está alojado. Nos estamos refiriendo a la IP local, es decir, privada. La configuración de la dirección IP del servidor en
una máquina virtual depende del sistema operativo que estemos utilizando. A continuación, veremos algunos pasos para configurar la dirección IP 
en una máquina virtual con Windows Server. Como 

<a name="item1"></a>
## 1. Consigna del desafío

### Escenario Prueba - Roles en Windows Server

**Empresa:** TechSolutions Inc.

**Sector:** Desarrollo de software y servicios tecnológicos.

**Escenario:** TechSolutions Inc. está creciendo rápidamente y ha contratado a nuevos empleados en varios departamentos, incluidos Desarrollo,
Recursos Humanos (RRHH), y Ventas. La empresa necesita asegurar que los datos y recursos sensibles sean accesibles solo para aquellos que lo
necesiten, así como aplicar configuraciones específicas en los equipos de los usuarios según sus roles y departamentos.

**Requisitos:**

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
## 2. Configuraciones

### Configuraciones básicas del Servidor - Configuración de la IP

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

### Configuraciones de Roles Primarios ' Rol Active Directory

**Paso 1:** Accede al Administrador del Servidor
* Presiona Win + X y selecciona "Administrador del Servidor".

   IMAGEN
  
**Paso 2:** Agrega el Rol de Servicios de Dominio de Active Directory
* En el Administrador del Servidor, selecciona "Agregar roles y características".

      Imagen
  
* En el asistente para agregar roles, selecciona "Servicios de Rol" y elige "Servicios de Dominio de Active Directory".

      Imagen
  
* Haz clic en "Siguiente" y luego en "Instalar". Sigue los pasos para completar la instalación del rol.

**Paso 3:** Configura AD DS
* Después de instalar el rol, aparecerá una notificación. Haz clic en "Promocionar este servidor a controlador de dominio".

     Imagen
* Selecciona la opción "Agregar un nuevo bosque" y proporciona el nombre de dominio deseado (por ejemplo, midominio.local).

     Imagen
  
* Establece una contraseña para la base de datos de AD DS y haz clic en "Siguiente".

     Imagen

* En la página "Funcionalidad del bosque", elige el nivel de funcionalidad adecuado para tus necesidades y haz clic en "Siguiente".
* En la página "Ubicación de archivos de base de datos", elige la ubicación de los archivos de base de datos de AD DS y haz clic en "Siguiente".
* Revisa la configuración en la página de resumen y haz clic en "Siguiente" para iniciar la instalación.

### Configuraciones de Dominio de Active Directory

**Paso 1:** Configura AD DS
* Después de instalar el rol, aparecerá una notificación. Haz clic en "Promocionar este servidor a controlador de dominio".

     Imagen
* Selecciona la opción "Agregar un nuevo bosque" y proporciona el nombre de dominio deseado (por ejemplo, midominio.local).

     Imagen
  
* Establece una contraseña para la base de datos de AD DS y haz clic en "Siguiente".

     Imagen

* En la página "Funcionalidad del bosque", elige el nivel de funcionalidad adecuado para tus necesidades y haz clic en "Siguiente".
* En la página "Ubicación de archivos de base de datos", elige la ubicación de los archivos de base de datos de AD DS y haz clic en
  "Siguiente".
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

     Imagen
  
### Configuraciones en dispositivos Clientes

### Organización jerárquica de AD


    
