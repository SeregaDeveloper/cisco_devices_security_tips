### Настройка пароля на переход в привелегированный режим

```
> en 
> conf t
> enable secret <password>
> end
> wr mem

```

### Создание администратора

```
> en 
> conf t
> aaa new-model
> username <admin> secret <password>
> end
> wr mem

```

### Настройка виртуального терминала

```
> en 
> conf t
> line vty 0 15
> privellege level 15
> end
> wr mem

```

### Настройка подключения по SSH

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
