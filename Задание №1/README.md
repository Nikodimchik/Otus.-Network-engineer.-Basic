# Задание
### [1. Построить простую топологию, используя Ethernet-кабель локальной сети.](#1)
### [2. Получить доступ к коммутатору Cisco, используя консольное подключение и методы удаленного доступа.](#2)
### [3. Проверить настройки коммутатора по умолчанию.](#3)
### [4. Настроить базовые параметры коммутатора.](#4)
### 5. Использовать IP-адрес управления для удаленного управления коммутатором.
# Решение
### <a name="1"> 1. Построить простую топологию, используя Ethernet-кабель локальной сети</a>

<image src="./Simple topology.PNG" alt="Простая топология сети.">

### <a name="2"> 2. Получить доступ к коммутатору Cisco, используя консольное подключение и методы удаленного доступа.</a>

  1. <image src="./Console.PNG" alt="Подключение консольным кабелем.">
  
  2. <image src="./cli.PNG" alt="Окно коммандной оболочки IOS.">
  
### <a name="3"> 3. Проверить настройки коммутатора по умолчанию.</a>
  *Switch>enable*  
     *Switch#show startup-config*  
   >startup-config is not present
  
### <a name="4"> 4. Настроить базовые параметры коммутатора.</a>
  *Switch#configure terminal*
  * ###### Задаём имя коммутатору.
    *Switch(config)#hostname C1*
  * ###### Задаём пароль рута на вход.
    *C1(config)#enable secret class*
  * ###### Задаём пароль для виртуальных терминалов и закодируем его.
    *C1(config)#line vty 0 15*  
    *C1(config)#password cisco*  
    *C1(config)#end*  
    *C1#configure terminal*  
    *C1(config)#service password-encryption*  
  * ###### Изменим баннерное сообщение.
    *C1(config)#banner motd +Hello there! It's me C1!+*
  * ###### Зададим интерфейс VLAN.
    *C1(config)#interface vlan 1*  
    *C1(config-if)#ip address 192.168.1.100 255.255.255.0*  
    *C1(config-if)#end*    
  * ###### Перезапишем конфиг по умолчанию на текущий.
    *C1#copy running-config startup-config*  
    >Destination filename [startup-config]?  
    >Building configuration...  
    >[OK]  
  * ###### Перезагрузим коммутатор.
    *C1#reload      
