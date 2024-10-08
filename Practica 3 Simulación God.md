
### PCA
```bash
ifconfig <nombre> 192.168.20.13 netmask 255.255.255.0 up
```

### PCB
```bash 
ifconfig <nombre> 192.168.30.13 netmask 255.255.255.0 up
```


## Switch 1
```ciscoIOS
!Configuracion basicas de un switch
!Lab Redes II
!
enable
conf t
!Asignar un nombre distintivo al dispositivo
hostname S1
!Asignar un dominio de trabajo
ip domain-name lrc2.uaz.mx
!Deshabilitar la resolucion de nombres
no ip domain-lookup
!Diseniar un banner o una etiqueta de presentacion
banner motd $
[+]-----------------------[+]
 | LabRedes2 - CCNAv7 SRWE |
 | Practica - 3            |
 | 03 de semptiembre  2024 |
 | S1                      |
 | MAYOGI                  |
 | Acceso restringido !!!  |
[+]-----------------------[+]
$

!Asignar una password al nivel privilegiado
enable secret class

! 3. Configurar las lineas de acceso (admin), consola y terminales virtuales
line console 0
! - Se configura un password para consola
password cisco
login

line vty 0 15
password cisco
login 

exit

service password-encryption
end

copy running-config startup-config
```


## Switch 2
```ciscoIOS
!Configuracion basicas de un switch
!Lab Redes II
!
enable
conf t
!Asignar un nombre distintivo al dispositivo
hostname S2
!Asignar un dominio de trabajo
ip domain-name lrc2.uaz.mx
!Deshabilitar la resolucion de nombres
no ip domain-lookup
!Diseniar un banner o una etiqueta de presentacion
banner motd $
[+]-----------------------[+]
 | LabRedes2 - CCNAv7 SRWE |
 | Practica - 3            |
 | 03 de semptiembre  2024 |
 | S2                      |
 | MAYOGI                  |
 | Acceso restringido !!!  |
[+]-----------------------[+]
$

!Asignar una password al nivel privilegiado
enable secret class

! 3. Configurar las lineas de acceso (admin), consola y terminales virtuales
line console 0
! - Se configura un password para consola
password cisco
login

line vty 0 15
password cisco
login 

exit

service password-encryption
end

copy running-config startup-config
```



## SW1 VLANs

```
conf t 
vlan 10 
name Administracion

vlan 20
name Ventas

vlan 30
name Operaciones

vlan 999 
name ParkingLot

vlan 1000
name Nativo

interface fa0/6
switchport mode acces
switchport acces vlan 20


interface range fa0/2 - fa0/5
switchport mode acces
switchport acces vlan 999
shutdown

interface range fa0/7 - fa0/24
switchport mode acces
switchport acces vlan 999
shutdown

interface range g0/1 - g0/2
switchport mode acces
switchport acces vlan 999
shutdown

interface vlan 10
ip address 192.168.10.11 255.255.255.0
no shutdown

interface vlan 20
ip address 192.168.20.11 255.255.255.0
no shutdown

interface vlan 30
ip address 192.168.30.11 255.255.255.0
no shutdown

```

### SW2 VLANs
```ciscoIOS
conf t 
vlan 10 
name Administracion

vlan 30
name Operaciones

vlan 999 
name ParkingLot

vlan 1000
name Nativo

! - Asignar el puerto 18 a la VLAN 30
interface fa0/18
switchport mode acces
switchport acces vlan 30


interface range fa0/2 - fa0/17
switchport mode acces
switchport acces vlan 999
shutdown

interface range fa0/19 - fa0/24
switchport mode acces
switchport acces vlan 999
shutdown

interface range g0/1 - g0/2
switchport mode acces
switchport acces vlan 999
shutdown

```

### Configurar puerto troncal en S1
```cicoIOS
conf t
interface fa0/1
switchport mode trunk
switchport trunk native vlan 1000
switchport trunk allowed vlan 10,20,30,1000
end 
show interfaces trunk

```

### Configurar puerto troncal en S2
```
conf t
interface fa0/1
switchport mode trunk
switchport trunk native vlan 1000
switchport trunk allowed vlan 10,20,30,1000
end 
show interfaces trunk
```
