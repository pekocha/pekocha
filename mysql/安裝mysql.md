**在alpine安裝SQL**
==
1.`sudo apk update`   
2.`sudo apk add mysql mysql-client`  
3.`sudo rc-service mariadb status`   
確認status的狀態，此時為關閉狀態  
4.`sudo nano /etc/my.cnf.d/mariadb-server.cnf`   
[mysqld]    
#skip-networking  
[galera]
bind-address=0.0.0.0

把skip-networking加上#，bind-address=0.0.0.0的#刪除  

7.`sudo /etc/init.d/mariadb setup`   
建立MySQL資料庫，同時電腦會幫你建立root跟mysql帳號  
8.`sudo rc-service mariadb start`  
啟動mariadb服務  
9.`sudo mysql` 成功進入服務  


