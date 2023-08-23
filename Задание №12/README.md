# Задание
### [1. Создать сеть согласно топологии и произвести базовую настройку оборудования.](#1)
### [2. Настройка сетей VLAN на коммутаторах.](#2)
### [3. Настройка и проверка PAT для IPv4.](#3)
### [4. Настройка и проверка статического NAT для IPv4.](#4)

# Решение   
### <a name="1"> 1. Создать сеть согласно топологии и произвести базовую настройку оборудования.</a>  

<image src="./scheme.PNG" alt="Configuration.">  
  
### <a name="2"> 2. Настроим NAT на R1, используя пул из трех адресов 209.165.200.226-209.165.200.228.</a>  

> R1:access-list 1 permit 192.168.1.0 0.0.0.255  
> R1:ip nat pool PUBLIC_ACCESS 209.165.200.226 209.165.200.228 netmask 255.255.255.248  
> R1:ip nat inside source list 1 pool PUBLIC_ACCESS  
> R1:interface g0/0/1  
> R1:ip nat inside  
> R1:interface g0/0/0  
> R1:ip nat outside  
> PC-B:ping 209.165.200.225  
> R1:show ip nat translations  

<image src="./trans1.PNG" alt="Dynamic1.">  

  *Внутренний адрес PC-B был транслирован в один из адресов нашего пула. Так как одноименный порт на R1 занят не был, то он и был транслирован порту на PC-B.*

> PC-A:ping 209.165.200.1  
> R1:show ip nat translations  

<image src="./trans2.PNG" alt="Dynamic2."> 

> S1:ping 209.165.200.1  
> R1:show ip nat translations  

<image src="./trans3.PNG" alt="Dynamic3.">  

>S2:ping 209.165.200.1  

  *Сообщения на R1 я не увидел, однако результат пинга был: U.U.U*  

### <a name="3"> 3. Настройка и проверка PAT для IPv4.</a>  

> R1:ip nat inside source list 1 pool PUBLIC_ACCESS overload  
> PC-B:ping 209.165.200.1  
> R1:show ip nat translations  

<image src="./pat1.PNG" alt="Pat.">  

> PC-A:ping 209.165.200.1  
> show ip nat translations  

<image src="./pat2.PNG" alt="Pat."> 

> R1:show ip nat translations verbose  

<image src="./verb.PNG" alt="verb.">  

> PC-A,PC-B,S1,S2:ping 209.165.200.1  

<image src="./pat3.PNG" alt="Pat.">  

> R1:ip nat inside source list 1 interface g0/0/0 overload  
> PC-A,PC-B,S1,S2:ping 209.165.200.1  

<image src="./pat2_1.PNG" alt="Pat.">

### <a name="4"> 4. Настройка и проверка статического NAT для IPv4.</a>  

> R1:ip nat inside source static 192.168.1.2 209.165.200.229  
> R1:show ip nat translations  

<image src="./static1.PNG" alt="Static.">  

> PC-A:ping 209.165.200.1  
> R1:show ip nat translations  

<image src="./static2.PNG" alt="Static.">  

