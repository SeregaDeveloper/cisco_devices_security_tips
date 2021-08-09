# Примеры безопасной настройки сетевого оборудования Cisco

## Содержание

   1. [Настройка защиты от несанкционированного доступа](#1-Настройка-защиты-от-несанкционированного-доступа)
      - 1.1 [Настройка пароля на переход в привелегированный режим](#11-Настройка-пароля-на-переход-в-привелегированный-режим)
      - 1.2 [Создание администратора](#12-Создание-администратора)
      - 1.3 [Настройка виртуального терминала для удаленного администрирования](#13-настройка-виртуального-терминала-для-удаленного-администрирования)
      - 1.4 [Настройка подключения по SSH](#14-Настройка-подключения-по-SSH)
      - 1.5 [Разрешение подключения только по SSH](#15-Разрешение-подключения-только-по-SSH)
      - 1.6 [Ограничение подключений к портам](#16-Ограничение-подключений-к-портам) 

## 1. Настройка защиты от несанкционированного доступа

### 1.1 Настройка пароля на переход в привелегированный режим

```
> en 
> conf t
> enable secret <password>
> end
> wr mem
```

### 1.2 Создание администратора

```
> en 
> conf t
> aaa new-model
> username <admin> secret <password>
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
> hostname <sw_example_name>
> ip domain-name <test.org
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

### 1.6 Ограничение подключений к портам

```
> en 
> conf t
> int range f0/1-24 
> switchport mode access
> switchport port-security violation shutdown 
> switchport port-security maximum <3>
> switchport port-security mac-address sticky
> end
> wr mem
```

### 1.7 Защита от подключений к неиспользуемым портам

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
