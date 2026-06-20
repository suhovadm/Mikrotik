Как настроить QinQ на Микротике?  


1) Interfaces – VLAN – (+)  

2) Создаём первый VLAN (верхнюю метку)  
	Name: VLAN1000  
	VLAN ID: 1000  
	Interface: ether4 (например)  
	Ставим галочку: Use service tag  
	Comment: Внешний VLAN (S-VLAN)  
 
3) Создаём второй VLAN (нижнюю метку)  
	Name: VLAN100  
	VLAN ID: 100  
	Interface: VLAN1000 (пристёгиваем 100-й VLAN к 1000-му)  
	Галочки Use service tag быть НЕ ДОЛЖНО!  
	Comment: Внутренний VLAN (C-VLAN)  

4) Пишем IP-шник:  
	IP – Addresses – (+)  
	Address: 10.0.0.1/24  
	Network: 10.0.0.0  
	Interface: VLAN100 (IP-адрес назначается на вложенный VLAN, а не основной)  
	Comment: IP for QinQ  

5) Как проверить?  
Открываем терминал Микротика и пишем:  

/interface vlan print  
/interface ethernet print  

Либо через сам Winbox.  
Interfaces – VLAN и рядом с QinQ VLAN-ами будет буковка «R» что означает «Running», то есть «Запущен/Работает».  
