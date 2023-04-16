# Задание
### [1. Настроить маршрутизатор.](#1)
### [2. Настроить компьютер PC-A и проверить соединение.](#2)
### [3. Настройка маршрутизатора для доступа по протоколу SSH.](#3)
### [4. Настройка основных параметров коммутатора.](#4)
### [5. Настройка коммутатора для соединения по протоколу SSH.](#5)
### [6. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора.](#6)
### [7. Вопрос для повторения.](#7)
# Решение  
<image src="./conf.PNG" alt="Configuration.">  
 
### <a name="1"> 1. Настроить маршрутизатор.</a>  
  * enable  
  * conf t  
  * no ip domain-lookup  
  * enable password class  
  * enable secret cisco  
  * line vty 0 15  
  * password cisco  
  * end  
  * conf t  
  * service password-encryption  
  * banner motd +You shel not pass!!! Anauyhorized access forbiden!+  
  * interface G0/0/1  
  * ip address 192.168.1.1 255.255.255.0  
  * no shutdown  
  * end  
  * copy running-config startup-config  
### <a name="2"> 2. Настроить компьютер PC-A и проверить соединение.</a>  
  <image src="./pc-ping-r1.png" alt="Настройка PC-a.">  

  
### <a name="3"> 3. Настройка маршрутизатора для доступа по протоколу SSH.</a>  
  * conf t
  * hostname R1  
  * ip domain-name otus.ru
  * crypto key generate rsa general-keys modulus 1024  
  * ip ssh version 2 
  * username admin secret Adm1nP@55 
  * line  vty 0 15  
  * transport input ssh  
  * login local  
  * end  
  * copy running-config startup-config  
  * SSH подключение с PC-A  
  <image src="./pc-ssh.png" alt="SSH PC-a.">   
    
 
### <a name="4"> 4. Настройка основных параметров коммутатора.</a>
  * enable  
  * conf t  
  * no ip domain-lookup  
  * enable password class  
  * enable secret cisco  
  * line vty 0 15  
  * password cisco  
  * end  
  * conf t  
  * service password-encryption  
  * banner motd +You shel not pass!!! Anauthorized access forbiden!+  
  * interface vlan 1 
  * ip address 192.168.1.11 255.255.255.0  
  * no shutdown  
  * end  
  * copy running-config startup-config  
### <a name="5"> 5. Настройка коммутатора для соединения по протоколу SSH.</a>  
  * conf t
  * hostname S1  
  * ip domain-name otus.ru
  * crypto key generate rsa general-keys modulus 1024  
  * ip ssh version 2 
  * username admin secret Adm1nP@55 
  * line  vty 0 15  
  * transport input ssh
  * transport input telnet
  * login local  
  * end  
  * copy running-config startup-config  
  * SSH подключение с PC-A  
  <image src="./pc_ssh_right.PNG" alt="SSH PC-a.">   
    
### <a name="6"> 6. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора.</a>  
  <image src="./s1-ssh.png" alt="SSH PC-a.">  
    
### <a name="7"> 7.Вопрос для повторения.</a>
     Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?
     *Необходимо добавить в локальную базу всех имеющихся пользователей.*
