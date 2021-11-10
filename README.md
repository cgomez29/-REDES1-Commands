# Redes de computadors 1


<div id='id0' />

## **Índice**   
1. [Guardar configuraciones](#id1)
2. [VPC](#id2)
3. [Switch](#id3)
4.  [Modo truncal](#id4)
5.  [Modo acceso](#id5)
6.  [VLAN](#id6)
7.  [VTP](#id7)
8.  [STP](#id8)
9.  [Port-Channel](#id9)
10.  [Router](#id10)
11.  [Configuracion de enlace](#id11)
12.  [HSRP](#id12)
13.  [GLBP](#id13)
14.  [Router on a Stick](#id14)
15.  [RIPv2](#id15)
16.  [OSPF](#id16)
17.  [EIGRP](#id17)
18.  [Redistribución](#id18)



<div id='id1' />

# Guardar configuraciones
### VPC

```console
   save
```

### Router or Switch

```console
   write # wr
```

[Volver](#id0)

<div id='id2' />

# VPC 

### Configuración de IP

```console
    ip 192.168.X.X 255.255.255.0 192.168.X.X
```

### Mostrar configuración

```console
    sh ip
```
[Volver](#id0)
<div id='id3' />

# Switch

<div id='id4' />

## Configurando modo de truncal

```console
    configure terminal
    int f#/# (ejemplo f1/1)
    Switchport mode trunk
    Switchport trunk allowed vlan 1,#vlan, 1002-1005
```

### Comando para vizualizar los puertos que estan en modo truncal

```console
    show interfaces trunk
```
[Volver](#id0)
<div id='id5' />

## Configurando modo de acceso

```console
    configure terminal 
    interface f#/# 
    switchport mode access 
    switchport access vlan #vlan
```

### Comando para verficar la correcta asignación del puerto en modo acceso
```
    show vlan-sw
```

[Volver](#id0)
<div id='id6' />


## VLAN 

```console
    configure terminal 
    vlan #
    name [name]
    end
```

### En donde # es el numero de la vlan a crear
### y [name] es nombre que la identificara.

<br>

### Comando para visualizar la configuración de la VLAN
```console
    show vlan-sw
```
### ó
```console
    vl
```
[Volver](#id0)
<div id='id7' />

## VTP


```console
    VTP
    conf t
    vtp domain [name}
    vtp password [password]
    vtp mode server/client/transparent
    sh vtp status


    VTP Pruning 
    conf t 
    vtp pruning
    end 

```

### Configuración del switch server

```console
    VTP
    configure terminal
    vtp domain grupo2
    vtp grupo2
    vtp mode server
    end
```

### Configuración del switch client

```console
    VTP
    configure terminal
    vtp domain grupo2
    vtp grupo2
    vtp mode client
    end
```

### VTP Pruning 

```console
    conf t 
    vtp pruning
    end 

```


### Comando para visualizar la configuración del VTP
```console
    show vtp status
```
[Volver](#id0)
<div id='id8' />

## Configuracion del Spannig Tree Protocol (STP)
### Sobre el switch server

```console
    configure terminal
    spannig-tree vlan # root primary
```
### verificar el Switch root 
```console
    show spannig-tree root
```
### Verificar STP 
```console
    show spanning-tree brief
```

### Puertos bloqueados
```console
    show spannig-tree blockedports
```

[Volver](#id0)
<div id='id9' />

## Port-Channel


```console
    conf t
    interfaces range f#/# - #
    channel-group # mode on 
    end
```

### Mostrar configuración
```console 
    show etherchannel port-channel
    show etherchannel summary
```

[Volver](#id0)
<div id='id10' />


# Router

<div id='id11' />


## Configuracion de enlace
```Console
    conf t
    int f#/#
    ip address [ip] [mask]
    no shutdown
    end
    wr
```

## Resumen de las ips configuradas
```console
    sh ip int brief
```

[Volver](#id0)
<div id='id12' />

## HSRP
### Router activo
```console
    conf t
    int f#/#
    standby # ip #IP
    standby # priority #
    standby # preempt
    end
```

### Router Standby
```console
    conf t
    int f#/#
    standby # ip #IP
    end
```

### mostrar configuración
```console
    sh standby
    sh standby brief
```


[Volver](#id0)
<div id='id13' />

## GLBP
### Router activo
```console
    conf t
    int s#/#
    glbp # ip #IP
    glbp # preempt
    glbp # priority #
    glbp # load-balancing #tipo de balanceo
    end
```

### Router Standby
```console
    conf t
    int s#/#
    glbp # ip #IP
    glbp # load-balancing #tipo de balanceo
    end
```

### mostrar configuración
```console
    sh glbp
    sh glbp brief
```

[Volver](#id0)

<div id='id14' />

##  Router on a Stick
### Configuración
```console
    conf t
    no shutdown
    int f#/#.#
    end
```

```console
    conf t
    int f#/#.#
    end
```

```console
    conf t
    int f#/#.#
    encapsulation dot1Q #
    ip address #ip #mask
    end
```

### mostrar configuración
```console
    sh ip interfaces brief
    sh run
    sh int f#/#.#
    sh ip arp
```
[Volver](#id0)

<div id='id15' />

# RIPv2
### Configuración
```console
    conft
    router rip
    version 2
    network "ip"
    end
```
### mostrar configuración

```console
    sh ip ro
```

[Volver](#id0)

<div id='id16' />

## OSPF
```console
    Comandos:
        1. config t
        2. router osfp 'area_ID'
        2. network 'IP' 'WILDCARD' area 'ID'
        3. end 
        4. wr
```

[Volver](#id0)

<div id='id17' />

## EIGRP
```console
    Comandos:
        1. config t
        2. router eigrp 'ID'
        2. network 'IP' 'WILDCARD' 
        2. no auto-summary
        3. end 
        4. wr
```

[Volver](#id0)

<div id='id18' />

## REDISTRIBUCION ENTRE PROTOCOLOS DE RUTEO DINAMICO
```console
    RIP - (OSPF & EIGRP)
        Comandos:
            1. config t
            2. router rip 
            3. redistribute ospf 'id' metric 'numero_saltos'
            4. redistribute eigrp 'id' metric 'numero_saltos'

    OSPF - (RIP & EIGRP)
        Comandos:
            1. config t
            2. router ospf 'id'
            3. redistribute rip subnets
            4. redistribute eigrp 'id' subnets

    EIGRP - (RIP & OSPF)
        Comandos:
            1. config t
            2. router eigrp 'id'
            3. redistribute rip metric 'Bandwith' 'Delay' 'Reliability' 'Bandwith' 'MTU'
            4. redistribute ospf 10 metric 'Bandwith' 'Delay' 'Reliability' 'Bandwith' 'MTU'

        Nota:
            La redistribución con EIGRP es la más complicada, ya que se deben de
            configurar 5 parámetros específicos. En nuestro caso utilizaremos los
            valores por defecto que recomiendan.

            1. Redistribute rip metric 10000 100 255 1 1500
            2. Redistribute ospf 10 metric 10000 100 255 1 1500
```

[Volver](#id0)