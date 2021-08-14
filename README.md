# Примеры безопасной настройки сетевого оборудования Cisco

## Содержание

   1. [Настройка защиты от несанкционированного доступа](#1-Настройка-защиты-от-несанкционированного-доступа)
      - 1.1 [Настройка пароля на переход в привелегированный режим](#11-Настройка-пароля-на-переход-в-привелегированный-режим)
      - 1.2 [Создание администратора](#12-Создание-администратора)
      - 1.3 [Настройка виртуального терминала для удаленного администрирования](#13-настройка-виртуального-терминала-для-удаленного-администрирования)
      - 1.4 [Настройка подключения по SSH](#14-Настройка-подключения-по-SSH)
      - 1.5 [Разрешение подключения только по SSH](#15-Разрешение-подключения-только-по-SSH)
      - 1.6 [Защита от подключений к неиспользуемым портам](#16-Защита-от-подключений-к-неиспользуемым-портам) 
   2. [Настройка защиты от компьютерных атак](#2-Настройка-защиты-от-компьютерных-атак)
      - 2.1 [Защита от атаки на протокол STP](#21-Защита-от-атаки-на-протокол-STP)
      - 2.2 [Защита от подмены MAC-адреса (MAC Spoofing)](#22-Защита-от-подмены-MAC-адреса-(-MAC-Spoofing-)-)

## 1. Настройка защиты от несанкционированного доступа

### 1.1 Настройка пароля на переход в привелегированный режим

```
> en 
> conf t
> enable secret password
> end
> wr mem
```

### 1.2 Создание администратора

```
> en 
> conf t
> aaa new-model
> username admin secret password
> end
> wr mem
```

### 1.3 Настройка виртуального терминала для удаленного администрирования

```
> en 
> conf t
> line vty 0 15
> privellege level 15
> end
> wr mem
```

### 1.4 Настройка подключения по SSH

```
> en 
> conf t
> hostname sw_example_name
> ip domain-name test.org
> crypto key generate rsa
> 1024
> [Enter]
> end
> wr mem
```

### 1.5 Разрешение подключения только по SSH

```
> en 
> conf t
> line vty 0 15 
> transport input ssh
> end
> wr mem
```

### 1.6 Защита от подключений к неиспользуемым портам

```
> en 
> conf t
> int range f0/1-24 
> vlan 999
> name Unconnected
> exit
> int range f0/1-24
> switchport mode access vlan 999
> shutdown
> end
> wr mem
```

## 2. Настройка защиты от компьютерных атак

### 2.1 Защита от атаки на протокол STP

```
> en 
> conf t
> int range f0/1-24 
> spanning-tree portfast
> spanning-tree portfast bpguard default
> int f0/1
> spanning-tree guard root
> end
> wr mem
```

### 2.2 Защита от подмены MAC-адреса (MAC Spoofing)

### Метод жесткой привязки по MAC

```
> en 
> conf t
> int f0/1
> switchport port-security mac-address xx:xx:xx:xx:xx:xx
> end
> wr mem
```

### Метод c привязкой нескольких MAC-адресов

```
> en 
> conf t
> int f0/1
> switchport port-security mac-address sticky
> switchport port-security maximum 3
> arp timeout 60
> end
> wr mem
```

