# Примеры безопасной настройки сетевого оборудования Cisco

## Содержание

   1. [Настройка защиты от несанкционированного доступа](#1.-Настройка-защиты-от-несанкционированного-доступа)


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
```
