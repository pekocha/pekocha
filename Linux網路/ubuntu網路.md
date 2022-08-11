**ubuntu固定IP設定**
===================
1.下指令 ```sudo nano /etc/netplan/00-installer-config.yaml``` 去更改設定檔  
(alpine是 sudo nano /etc/network/interfaces)  

2.在ens32下做縮排分別輸入  
addresses: [(設定的IP位子)/24(網路遮罩)]  
gateway: (設定的IP位子)  
nameservers:  
    addresses: [8.8.8.8]  
(名稱伺服器可以不只一組)  

3.在dhcp4那打上#做註解取消功能  
之後按ctrl+o做儲存 ENTER確定 ctrl+x 離開  

4.出來畫面後輸入```sudo netplant apply```做網路的**暫時**套用(重開機可永久套用)
套用完可以使用ping指令ping回gateway4或是8.8.8.8(GOOGLE)看看確認是否可以上網

**確認連線狀況**
===============
1.檢查自己IP  
2.PING GATEWAY  
3.PING 外面的網站(例如8.8.8.8 GOOGLE)  
