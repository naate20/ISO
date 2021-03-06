- Hostname:
- IP: Automática/Dinámica(DHCP) ó Estática (dirección ip, máscara, puerta de enlace, dns's)

Dirección de red: 192.168.0.0 / 16

Máscara: 192.168.0.100

DNS: 1.1.1.1     1.0.0.1

- A tener en cuenta al configurar un ordenador:

    - Nombre
    - red
    - Actualizaciones
    - Zona horaria
    - Cortafuegos y antivirus
    - Usuarios
    - Servicios
    - Software


> COMANDOS:
    - hostname: nombre del equipo  
    - ipconfig: información sobre la configuración de red  
    -c ambiar nombre por consola: Rename-Computer -NewName  [newName]

- Powershell: Intérprete de comandos que sustituye a CMD (Procede de MSDOS). Tiene ayuda integrada con el comando: Get-Help  
    - Comandos -> Commandlets (nomenclatura explícita)
    - Scripting 
    - Bases de Datos

- Formato de los Commandlets:  
    PROMPT (c:\...) + Commandlet + [parámetros/opciones [values]]  
    - Ejemplo: c:\...> Get-Help New-LocalUser Mostrará la ayuda de New-LocalUser.


- Crear un usuario local: 
    - New-LocalUser -Name jdoe -Fullnanme "John Doe"  -PasswordNeverExpires -Password (Convertto-SecureString) [...]

DEBERES: buscar como cambiar la configuración de red desde el Powershell


 Get-DnsClientServerAddress command to show InterfaceAlias
 Set-DNSClientServerAddress "InterfaceAlias" –ServerAddresses ("preferred-DNS-address", "alternate-DNS-address")  -> to change IPv4 and IPv6 addresses.

 It requires you to change three things before hitting the Enter button:

    InterfaceAlias,
    Preferred-DNS-address,
    Alternate-DNS-address.

    Before pressing the Enter button, it would look like this-
        Set-DNSClientServerAddress "Wi-Fi" –ServerAddresses ("1.1.1.1","1.0.0.1")
    

New-NetIPAddress –InterfaceAlias “Wired Ethernet Connection” –IPv4Address “192.168.0.1” –PrefixLength 24 -DefaultGateway 192.168.0.254



- Get-NetAdapter : lo empleamos para ver el nombre y el índice de la red

- APIPA (Automatic Private IP Addressing): direccion que se autoadjudica windows cuando no le pasamos una configuración 


## USUARIOS Y GRUPOS:

- Usuario: Perfil con el que un humano va a acceder al equipo. Tendrá:  
    - Login (username) sam account name
    - Password
    - Home: carpeta de trabajo del usuario.

- El administrador gestiona todo. Pone el usuario y la contraseña.

- Además, los usuarios pertenecen a grupos (conjunto de usuarios para establecer permisos). 2 grupos bases: Administrators & Users.

- Al instalar el SO, creamos un usuario, este pertenecerá al grupo de administradores, además del propio usuario Administrator, que está deshabilitado
por motivos de seguridad.


> Crear un nuevo usuario local  
New-LocalUser -Name nombre -PasswordNeverExpires -Password (ConvertTo-SecureString) [...]

> Añadir usuario a grupo  
Add-LocalGroupMember -Group [group_name] -Member [member_name]

> Borrar puerta de enlace:  
remove-netroute -Confirm:$false

### CREAR GRUPOS Y USUARIOS POR PANEL DE CONTROL

Action > New Group...  
    Nombre  
    [Descripción]  
    Si ya tenemos usuarios creados podemos añadirlos en el botón Add

Sería lo mismo para los usuarios, hay que estar en la carpeta correspondiente.

    username
    Fullnanme
    [Descripción]

    Password 
    confirm Password

    Selección de la configuración de la contraseña.

Para poder acceder a su cuenta, el usuario tiene que estar en el grupo Users 

### CREAR GRUPOS Y USUARIOS POR COMANDOS

Utilizaremos localuser y localgroup   

Para poder utilizar scripts:

> Set-ExecutionPolicy Unrestricted -Scope LocalMachine

## Creación de una atrea básica:

Nos deja configurar 4 aspectos:
- Nombre
- Descripción
- Trigger
- Acción

> %SystemRoot% -> tiene la instalación de windows  
  Cuando van entre dos tantos por ciento son variables de entorno



  # Servicios
 El comando stop-service solo detiene el servicio en ese momento pero al volver a arrancar la máquina se vuelve a habilitar.  
 Para que el servicio no se vuelva a ejecutar sería el comando Stop-Service, pero si quisiéramos que no vuelva a habilitarse y que se detenga en ese momento, tenemos que lanzar ambos comandos.

 ---------------------------------------------------------------------------------------------------------------------

Repositorios que utlizia:
- msstore
- github


Instalar brave:

> winget search brave
>winget install --name brave --source winget

Sería lo mismo para el powershell
> winget search powershell
> winget install --Name powershell --source winget

 ---------------------------------------------------------------------------------------------------------------------

 Archivo: Conjunto de datos. Texto, ejecutables, binarios, links (enlaces)
 Carpeta (directorio) : Contenedor de archivos y carpetas

 La estructura es jerárquica

 C:\ -> Raíz

 En powershell:
 - Item: Archivo / Carpeta
 - Clear-Item
 - Copy-Item
 - Move-Item
 - New-Item
 - Remove-Item
 - Rename-Item
 - Get-ChildItem -> dir (cmd)
    - Con el atributo Recurse se muestra todo lo que hay desde el directorio donde estamos hasta el nivel más bajo
- tree nos da la información en árbol del directorio que le indiquemos

- Ruta (PATH): forma de llegar al archivo. Hay rutas absolutas (como llegar desde la raíz) y rutas relativas (como llegar desde mi ubicación).

> Write-Output -> devuelve la ruta

> Test-Path -> Devuelve true o false si la ruta existe  o no respectivamente  
    
Volver a la raiz:  
    - cd C:\
    - cd ..\..\

   
    
cd = Set-Location  
  
ls = Get-ChildItem  
  
Crear un directorio:

- mkdir = New-Item   


> PS C:\Users\user\Documents> New-Item -Name foodir

    Directory: C:\Users\user\Documents

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a---          29/11/2021    12:51              0 foodir

PS C:\Users\user\Documents>

> PS C:\Users\user\Documents> New-Item -Name reallyfoodir   -ItemType Directory
    Directory: C:\Users\user\Documents
Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d----          29/11/2021    12:52                reallyfoodir


> PS C:\Users\user\Documents> mkdir reallyfoodir2
    Directory: C:\Users\user\Documents
Mode                 LastWriteTime         Length Name
d----          29/11/2021    12:53                reallyfoodir2

Eliminar un directorio:   
- Remove-Item [Path] <string[]>  
  
- Remove-Item -LiteralPath <string[]>   

New-Item -Path .\reallyfoodir\ -Name otherdir -ItemType Directory

> MIMETYPE: especifica el tipo de contenido de un archivo (cabecera)


> PS C:\Users\user\Documents> Remove-Item -Path .\reallyfoodir\ -Recurse -Force

> PS C:\Users\user\Documents> Remove-Item -Path .\reallyfoodir2\, .\foodir

## Borar un usuario y todos sus archivos

> Remove-LocalUser [name]    

> Remove-Item -Path [path] -Recurse -Force    

- no lo podemos borrar

- rmdir /s /q [ruta]
    - La s es el recurse
    - la q es el force
    - **CON CMD SI QUE PODEMOS**

> cmd /c rmdir /s /q [path]

cmd /c lanza el cmd para que ejecute el comando que va a continuación.

## Permisos de carpetas



ping funciona por el protocolo ICMT, echo request y echo reply cuando hacemos un ping

-New-NetFirewallRule -Name -Direction -Profile -Action -LocalPort -Protocol

