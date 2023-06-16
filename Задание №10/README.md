# Задание
### [1. Создать сеть согласно топологии и произвести базовую настройку оборудования.](#1)
### [2. Настройка и проверка базовой работы протокола OSPFv2 для одной области.](#2)
### [3. Реализация различных оптимизаций на каждом маршрутизаторе.](#3)
### [4.	Проверка оптимизации OSPFv2.](#4)

# Решение   
### <a name="1"> 1. Создать сеть согласно топологии и произвести базовую настройку оборудования.</a>  

<image src="./Conf.PNG" alt="Configuration.">  
  

### <a name="2"> 2. Настройка и проверка базовой работы протокола OSPFv2 для одной области.</a>  
  
  * R1(config)#router ospf 56  
  * R1(config-router)#router-id 1.1.1.1  
  * R1(config-router)#network 10.53.0.0 0.0.0.255 area 0  

  * R2(config)#router ospf 56  
  * R2(config-router)#router-id 2.2.2.2  
  * R2(config-router)#network 10.53.0.0 0.0.0.255 area 0  
  * R2(config-router)#network 192.168.1.1 0.0.0.255 area 0  
  
  Проверка смежности.  
  
  <image src="./r2-neighbor.PNG" alt="Проверка смежности.">  
   
  *R1 выступает в роли назначенного роутера, благодоря меньшему значению id.* 
    
  Таблица маршрутизации R1.
    
  <image src="./r1-route.PNG" alt="Таблица маршрутов R1."> 
    
  Ping до адреса интерфейса R2 Loopback 1 из R1.
    
  <image src="./r1-ping-loopback.PNG" alt="Пинг R1 - loopback R2.">  
    
### <a name="3"> 3. Реализация различных оптимизаций на каждом маршрутизаторе.</a>  
    
  Изменим приоритет интерфейса и таймер Hello сообщений.  
  * R1(config)#interface g 0/0/1  
  * R1(config-if)#ip ospf cost 50  
  * R1(config-if)#ip ospf hello-interval 30  
    
  * R2(config)#interface g 0/0/1  
  * R2(config-if)#ip ospf hello-interval 30  
    
 Настроим статический маршрут на R1 и поделимся им.  
    
  * R1(config)#ip route 0.0.0.0 0.0.0.0 Loopback1  
  * R1(config)#router ospf 56  
  * R1(config-router)#default-information originate  
    
  Добавим конфигурации для R2.
    
  * R2(config)#interface loopback1  
  * R2(config-if)#ip ospf network point-to-point  
  * R2(config)#router ospf 56  
  * R2(config-router)#passive-interface loopback1  
    
### <a name="4"> 4. Проверка оптимизации OSPFv2.</a>  
    
  <image src="./r1-ospf-check.PNG" alt="show ip ospf interface g0/0/1 на R1.">  
    
  <image src="./r1-route.PNG" alt="show ip route на R1.">  
    
  <image src="./r2-ospf-check.PNG" alt="show ip route на R2.">  
    
  <image src="./r2-ping-loopback.PNG" alt="Пинг R2 - loopback R1.">  
    
  
  
