# Задание
### [1. Создать сеть согласно топологии.](#1)
### [2. Настроить базовые параметры для маршрутизаторов.](#2)
### [3. Проверка назначения адреса SLAAC от R1.](#3)
### [4.	Настройка и проверка сервера DHCPv6 на R1.](#4)
### [5. Наблюдение за процессом выбора протоколом STP порта, исходя из приоритета портов.](#5)
### [6. Вопросы для повторения.](#6)

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
