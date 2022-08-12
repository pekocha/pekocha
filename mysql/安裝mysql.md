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

**設定 Mariadb 開機自動啟動**
==
1.`sudo rc-update add mariadb default`  
2.`rc-update show default | grep mariadb` 確認有沒有加入  
3.`sudo reboot`  
4.`sudo rc-service mariadb start` 重啟服務  

**Mariadb安全設定**
==
1.`sudo mysql_secure_installation`  
Enter current password for root (enter for none): Enter  
輸入目前root密碼(沒就按enter)  
..........  
Switch to unix_socket authentication [Y/n] y  
是否切換至unix_socket登入方式?(本地登入)  
..........  
Change the root password? [Y/n] y  
New password:root  
Re-enter new password:root  
是否修改root密碼?  
Remove anonymous users? [Y/n] y  
是否移除匿名使用者  
........  
Disallow root login remotely? [Y/n] y  
是否移除root的遠端登錄?(要，因為遠端root太危險)  
........  
Remove test database and access to it? [Y/n] y  
是否移除預設的資料庫?(要，因為沒用)  
.......  
Reload privilege tables now? [Y/n] y  
(要不要重新載入設定?)  
Thanks for using MariaDB!  

**登入SQL**
==
1.`mysql -u root -p`        使用root身分並輸入密碼   
2.`select current_user();`  目前登入MySQL的人有誰?    

**登入 MySQL - Socket 使用本地作業系統的帳號登入**   
==
sudo mysql -u root -S /run/mysqld/mysqld.sock   
             ||   
sudo mysql    
   
**新增 bigred 帳號可以從遠端登入**
==
1.`GRANT ALL PRIVILEGES ON *.* TO 'bigred'@'%' IDENTIFIED BY 'bigred' WITH GRANT OPTION;`  
讓bigred獲得在所有資料庫裡(*.*)的最高權限，可從所有的IP登入並且可以賦予他人權限  
2.`FLUSH PRIVILEGES;`   
給權限或是刪除權限時必定要加的指令  
3.`SELECT user,host FROM mysql.user;`   
查詢使用者的權限  
