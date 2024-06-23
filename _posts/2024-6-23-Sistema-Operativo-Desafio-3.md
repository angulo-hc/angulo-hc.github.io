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

<a name="item1"></a>
## 2. Configuraciones de servicios


    
