# Задание
### [1. Создать сеть согласно топологии и произвести базовую настройку оборудования.](#1)
### [2. Настройка сетей VLAN на коммутаторах.](#2)
### [3. Настройка маршрутизации между сетями VLAN на R1.](#3)
### [4. Настройка все сетевые устройства для базовой поддержки SSH.](#4)
### [5. Проверка подключения.](#5)  
### [6. Настройка и проверка списков контроля доступа (ACL).](#6)  

# Решение   
### <a name="1"> 1. Создать сеть согласно топологии и произвести базовую настройку оборудования.</a>  

<image src="./scheme.PNG" alt="Configuration.">  
  

### <a name="2"> 2. Настройка сетей VLAN на коммутаторах.</a>  

<image src="./vlan.PNG" alt="Vlan.">  

<image src="./trunk.PNG" alt="trunk.">  

### <a name="3"> 3. Настройка маршрутизации между сетями VLAN на R1.</a>  

<image src="./r1.PNG" alt="R1.">  

### <a name="4"> 4. Настройка все сетевые устройства для базовой поддержки SSH.</a>  

> username SSHadmin secret 5 $1$mERr$jnsDknF4Wwkgx2tzKw49w1  
> ip ssh version 2  
> ip domain-name ccna-lab.com  
> line vty 0 4  
> login local  
> transport input ssh  

### <a name="5"> 5. Проверка подключения.</a>  

| От | Протокол | Назначение | Отметка |
|----------|----------|----------|----------|
| PC-A | Ping | 10.40.0.10 | True |
| PC-A | Ping | 10.20.0.1 | True |
| PC-B | Ping | 10.30.0.10 | True |
| PC-B | Ping | 10.20.0.1 | True |
| PC-B | Ping | 172.16.1.1 | True |
| PC-B | HTTP | 10.20.0.100 | True |
| PC-B | SSH | 10.20.0.1 | True |
| PC-B | SSH | 172.16.1.1 | True |  

### <a name="6"> 6. Настройка и проверка списков контроля доступа (ACL).</a>  

  > interface GigabitEthernet0/0/1.40  
  > ip access-group MYLIST out

  > interface GigabitEthernet0/0/1.30  
  > ip access-group MYLIST2 out  

<image src="./ACL3.PNG" alt="ACL.">  

| От | Протокол | Назначение | Отметка |
|----------|----------|----------|----------|
| PC-A | Ping | 10.40.0.10 | False |
| PC-A | Ping | 10.20.0.1 | True |
| PC-B | Ping | 10.30.0.10 | False |
| PC-B | Ping | 10.20.0.1 | False |
| PC-B | Ping | 172.16.1.1 | True |
| PC-B | HTTP | 10.20.0.100 | False |
| PC-B | SSH | 10.20.0.1 | False |
| PC-B | SSH | 172.16.1.1 | True |  

