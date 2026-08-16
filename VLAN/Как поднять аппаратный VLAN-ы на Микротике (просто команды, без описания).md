Команды для создания VLAN в Микротике.  

1) /interface bridge  
2) add name=bridge2 vlan-filtering=yes  
3) /interface vlan  
4) add interface=bridge2 name=bridge2.10 vlan-id=10  
5) /interface bridge port  
6) add bridge=bridge2 interface=ether3 pvid=10  
7) add bridge=bridge2 interface=ether5 pvid=10 (это, если мы хотим закинуть в 10-й VLAN ещё и 5-й порт Микрота, но мы не хотим)  
8) /interface bridge vlan  
9) add bridge=bridge2 tagged=bridge2 untagged=ether3,ether5(этот не надо) vlan-ids=10  

10) /ip address  
11) add address=192.168.10.1/24 interface=bridge2.10 network=192.168.10.0  
12) /ip pool add name="pool10" ranges="192.168.10.2-192.168.10.254"  
13) /ip dhcp-server  
14) add address-pool=pool10 disabled=no interface=bridge2.10 name=dhcp10  
* На данном этапе заходим IP - DHCP Server - DHCP - dhcp10 - выставляем время аренды на сутки.  
* Дальше заходим во вкладку Networks - нажимаем на "+" и пишем:  
Address: 192.168.10.0/24  
Gateway: 192.168.10.1  
DNS: 192.168.10.1  
Всё остальное не надо - APPLY - OK.  
15) Всё, подключаемся к 3-у порту Микротика и проверяем, что VLAN10 работает.  
