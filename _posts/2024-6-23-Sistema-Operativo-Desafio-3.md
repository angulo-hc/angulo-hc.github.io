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
- [2. Configuración](#item2)
- [3. Solución del desafío](#item3)
- [4. Demo](#item4)


<a name="item1"></a>
## 1. Consigna del desafío

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
## 2. Configuraciones

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

        

### Configuraciones de Roles Primarios ' Rol Active Directory

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

<a name="item3"></a>
## 3. Solución del desafío

### Organización jerárquica de AD ##########################


### Creación de cuentas de unidades organizativas, usuario, grupos

A continuación, de acuerto a la especificación de nuestro escenario, proseguiremos a crear tres unidades organizativas, 
dentro de del domino *techsolutions*, en nuestro *AD*.

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

 **Paso 3:** Crear Usuarios y Grupos
* Dentro de cada *UO*, crea usuarios según la estructura organizativa. Haz clic derecho en la UO, 
  selecciona "Nuevo" y elige Usuario.

    ![CreacionUsuario_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_1.png) 

* Ingresa la información necesaria para cada usuario, como nombre, contraseña, etc.

    ![CreacionUsuario_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_2.png)

    ![CreacionUsuario_3]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionUsuario_3.png)

* Dentro de cada *UO*, crea un *grupo* según la estructura organizativa.

  ![CreacionGrupos_1]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionGrupos_1.png)

* Ingresa la información necesaria para cada grupo

  ![CreacionGrupos_2]({{ site.baseurl }}/images/Sistema_Operativo/Desafio_3/CreacionGrupos_2.png)


### Políticas de Grupo (GPO)


<a name="item4"></a>
## 4. Demo

    
