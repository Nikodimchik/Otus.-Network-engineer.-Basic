# Задание
### [1. Создать сеть согласно топологии.](#1)
### [2. Настроить базовые параметры для маршрутизаторов.](#2)
### [3. Проверка назначения адреса SLAAC от R1.](#3)
### [4.	Настройка и проверка сервера DHCPv6 на R1.](#4)
### [5. Настройка сервера DHCPv6 с сохранением состояния на R1.](#5)
### [6. Настройка R2 в качестве агента DHCP-ретрансляции.](#6)
### [7. Создание сети и настройка основных параметров устройств для реализации DHCPv4.](#7)
### [8. Проверка работы DHCPv4.](#8)

# Решение   
### <a name="1"> 1. Создать сеть согласно топологии.</a>  

<image src="./topology.PNG" alt="Configuration.">  
  
### <a name="2"> 2. Настроить базовые параметры для маршрутизаторов и коммутаторов.</a>  
  https://github.com/Nikodimchik/Otus.-Network-engineer.-Basic/blob/main/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%E2%84%968/S1-config.txt  
  https://github.com/Nikodimchik/Otus.-Network-engineer.-Basic/blob/main/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%E2%84%968/S2-config.txt  
  https://github.com/Nikodimchik/Otus.-Network-engineer.-Basic/blob/main/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%E2%84%968/R1-config.txt  
  https://github.com/Nikodimchik/Otus.-Network-engineer.-Basic/blob/main/%D0%97%D0%B0%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5%20%E2%84%968/R2-config.txt  
  
### <a name="3"> 3. Проверка назначения адреса SLAAC от R1.</a> 

<image src="./slaac-pcA.PNG" alt="SLAAC PC-A.">  

  * Часть адреса с идентификатором хоста была сгенерирована алгоритмом EUI-64 на основе MAC адреса.  
  
### <a name="4"> 4. Настройка и проверка сервера DHCPv6 на R1.</a>  
Создаем новый пул:  

  * R1(config)#ipv6 dhcp pool R1-STATELESS  
  * R1(config)#dns-server 2001:db8:acad::254  
  * R1(config)#domain-name STATELESS.com  
  
Настраивем интерфейс G0/0/1 на R1:  

  * R1(config-if)#ipv6 nd other-config-flag  
  * R1(config-if)#ipv6 dhcp server R1-STATELESS  
  
<image src="./r1-stateless.PNG" alt="IPCONFIG.">  
   
Для того, чтобы обеспечить Ip связанность пропишем маршруты на роутерах:  
    
  * R1(config)#ipv6 route 2001:db8:acad:3::/64 2001:db8:acad:2::2  
  * R2(config)#ipv6 route 2001:db8:acad:1::/64 2001:db8:acad:2::1  
  
<image src="./Ping-Stateless.PNG" alt="IPCONFIG.">  

### <a name="5"> 5. Настройка сервера DHCPv6 с сохранением состояния на R1.</a>  
Создаем новый пул с префиксом:  
  
  * R1(config)#ipv6 dhcp pool R2-STATEFUL  
  * R1(config)#address prefix 2001:db8:acad:3:aaa::/80  
  * R1(config)#dns-server 2001:db8:acad::254  
  * R1(config)#domain-name STATEFUL.com  
  
Настраивем интерфейс G0/0/0 на R1:  
  
  * R1(config-if)#ipv6 dhcp server R2-STATEFUL  
  
Проверка назначения адреса SLAAC на PC-B.  
  
<image src="./slaac-pc-B.PNG" alt="SLAAC на PC-B">   
  
### <a name="6"> 6. Настройка R2 в качестве агента DHCP-ретрансляции</a>  

  * R2(config-if)#ipv6 nd managed-config-flag  
  * R2(config-if)#ipv6 dhcp relay destination 2001:db8:acad:2::1 g0/0/0  

### <a name="7"> 7. Создание сети и настройка основных параметров устройств для реализации DHCPv4</a>  
  *Подсеть А: 192.168.1.0 255.255.255.192 - 1 адрес 192.168.1.1*  
  *Подсеть Б: 192.168.1.64 255.255.255.224 - 1 адрес 192.168.1.65*  
  *Подсеть В: 192.168.1.96 255.255.255.240 - 1 адрес 192.168.1.97*   
  S1  Config:  

<image src="./s1-vlan.PNG" alt="R1">   

  R1 Config:  

<image src="./n-r1v.PNG" alt="R1">  

  R2 Config:

<image src="./n-r2.PNG" alt="R1">  

  R1 DHCP настройки:  

<image src="./n-dhcp.PNG" alt="R1">  

### <a name="8"> 8. Проверка работы DHCPv4</a>  

  PC-A:  

<image src="./pc-a.PNG" alt="R1">  

  PC-B:  

<image src="./n-pc2.PNG" alt="R1">  

