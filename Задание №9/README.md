# Задание
### [1. Создать сеть согласно топологии и произвести базовую настройку оборудования.](#1)
### [2. Настройка сетей VLAN на коммутаторах.](#2)
### [3. Отключение согласование DTP G0/1 на S1 и S2х.](#3)
### [4. Настройка и проверка статического NAT для IPv4.](#4)  
### [5. Реализовать безопасность DHCP snooping.](#5)  
### [6. Реализовать PortFast и BPDU Guard.](#6)  
### [7. Проверка наличия сквозного ⁪подключения.](#7)  

# Решение   
### <a name="1"> 1. Создать сеть согласно топологии и произвести базовую настройку оборудования.</a>  

<image src="./scheme.PNG" alt="Configuration.">  
  
<image src="./R1-int.PNG" alt="R1.">  

### <a name="2"> 2. Настройка сетей VLAN на коммутаторах.</a>  

<image src="./s1-status.PNG" alt="Vlan.">  

<image src="./s1-trunk1.PNG" alt="Trunk.">  

### <a name="3"> 3. Отключение согласование DTP G0/1 на S1 и S2х.</a>  

<image src="./s1-nego.PNG" alt="Nonegotiation.">  

### <a name="4"> 4. Настройка и проверка статического NAT для IPv4.</a>  

<image src="./s1-port-sec.PNG" alt="Port-sec.">  

<image src="./s1-show-portsec.PNG" alt="Port-sec.">  

<image src="./s2-portsec-conf.PNG" alt="Port-sec.">  

<image src="./s2-show-portsec.PNG" alt="Port-sec.">  

<image src="./s2-show-addr.PNG" alt="Port-sec.">  

### <a name="5"> 5. Реализовать безопасность DHCP snooping.</a>  

  > ip dhcp snooping vlan 10  
  > ip dhcp snooping  

  > (if-config):ip dhcp snooping limit rate 5  

<image src="./s2-dhcp-snooping.PNG" alt="DHCP snooping.">  

<image src="./pc-b-dhcp1.PNG" alt="DHCP snooping.">  

<image src="./pc-b-dhcp2.PNG" alt="DHCP snooping.">  

### <a name="6"> 6. Реализовать PortFast и BPDU Guard.</a>  

<image src="./s2-portfast.PNG" alt="Portfast BPDUguard.">  

### <a name="7"> 7. Проверка наличия сквозного ⁪подключения.</a>  

| От | Протокол | Назначение | Отметка |
|----------|----------|----------|----------|
| PC-B | Ping | 192.168.10.1 | True |
| PC-B | Ping | 10.10.1.1 | True |
| PC-B | Ping | 192.168.10.201 | True |
| PC-B | Ping | 192.168.10.202 | True |
| PC-B | Ping | 192.168.10.10(DHCP) | True |
