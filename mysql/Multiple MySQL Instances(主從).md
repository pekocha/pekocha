Multiple MySQL Instances**
==
1.安裝mariadb本體
2.修改 Bash script: mysql_install_db    
sudo nano /usr/bin/mysql_install_db    
if false  
\# if test -n "$user"  
then  
  if test -z "$srcdir" -a "$in_rpm" -eq 0  
492行    
3.建立 MySQL 分身，登入使用者帳號rbean(沒有SUDO權限)  
4.mkdir /home/rbean/{lib,my.cnf.d,mysqld}  
建立三個資料夾  
lib      裝sqldata相關資訊  
my.cnf.d 裝cnf設定檔  
mysqld   裝sock檔跟pid檔  

5.mkdir ~/lib/mysqla  
創建一個分身a專用資料夾  
6.cp /etc/my.cnf.d/mariadb-server.cnf ~/my.cnf.d/mariadb-servera.cnf  
複製設定檔進來作修改  
7.nano ~/my.cnf.d/mariadb-servera.cnf  
更改設定檔，步驟參考下方  
8.mysql_install_db --user=rbean --datadir=/home/rbean/lib/mysqla/  
建立帳號rbean於剛剛創立的/lib/mysqla裡面  
此行命令相同於柔安老師ppt1地23頁的sudo /etc/init.d/mariadb setup  
9.mysqld_safe --defaults-file=/home/rbean/my.cnf.d/mariadb-servera.cnf &  
啟動MySQL，使用demon並加入指令&讓他在背景執行  
10.$ mysql -S ~/mysqld/mysqlda.sock  
進入系統  
11.grant all on *.* to 'root'@'localhost' identified by 'rbean' with grant option;  
讓root有對所有資料庫的資料有修改權限，可從localhost登入，密碼為rbean，並可賦予他人權限  
12.flush privileges;  
刷新更改  
13.mysql_secure_installation -S ~/mysqld/mysqlda.sock  
設定 MySQL 分身安全性  
    1、Enter current password for root (enter for none):  
   （輸入密碼）  
    2、Switch to unix_socket authentication [Y/n]  
   （ n，不切換到 unix_socket 身份驗證）  
    3、Change the root password? [Y/n]  
   （ n，不更換 root 密碼）  
    4、Remove anonymous users? [Y/n]  
   （ Y，移除匿名登入）  
    5、Disallow root login remotely? [Y/n]  
   （ Y，移除遠端 root 登入權限）  
    6、Remove test database and access to it? [Y/n]  
   （ Y，移除測試資料庫及帳號）  
    7、Reload privilege tables now? [Y/n]  
   （ Y，重新載入權限表）  
14.mysqladmin version -p -S ~/mysqld/mysqlda.sock  
檢查 MySQL 分身套件版本與服務運行狀態(rbean本人)  

mysqladmin version -u root -p -h 127.0.0.1 -P 3311  
使用在mysql裡的root(rbean)身分網路查看mysql資訊  
**網路登入需要密碼**  
15.mysql -u root -prbean -h 127.0.0.1 -P 3311  
網路登入，需要密碼，-p後緊連密碼。  
16.SHOW VARIABLES LIKE "char%";  
查詢 MySQL 分身編碼設定   
17.SHOW VARIABLES LIKE "coll%";  
查詢 MySQL 分身資料排序規則設定  

**mariadb設定檔**
==
skip-networking=0  
#把「取消外部連線」關閉，所以=0  
user=rbean  
#設定使用者  
pid-file=/home/rbean/mysqld/mysqlda.pid  
#pid會記錄mysqld的Daemon（在系統中，都會依照需求安裝許多服務，但這些服務本身並不會自動啟用，  
針對啟用服務程序，即稱為 Daemon），mysqld的Daemon啟動以後會有pid，  
它會把pid記錄在這個指定路徑底下的mysqlda.pid。假設要再啟動mysqld的Daemon，  
它會從mysqlda.pid裡面查詢，若裡面有數字代表mysqld的Daemon已經啟動了，  
所以就不會重複再啟動mysqld的Daemon。假設把Daemon關掉，mysqlda.pid裡面原本的pid數字也會跟著被消除，  
所以Daemon停掉再重開時，mysqlda.pid裡面是空的，就可以再啟動Daemon，  
再把新啟動的pid數字寫入mysqlda.pid。  

socket=/home/rbean/mysqld/mysqlda.sock  
#幫process之間資訊溝通的文件  
port=3311  
#本尊3306，額外設定port不要互搶以免無法開啟  
空port請查詢「TCP/UDP埠列表」  
datadir=/home/rbean/lib/mysqla  
#sqldata相關資訊存放位子  
character-set-client-handshake=FALSE  
#禁止根據客戶端做調整  
collation-server=utf8mb4_unicode_ci  
#排列功能比utf8mb4_general_ci精準但更耗能，因為是標準的Unicode排序  
init-connect='SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci'  
#跟DAEMON說我們編碼的伺服器名子是utf8mb4，排序使用utf8mb4_unicode_ci  
character-set-server=utf8mb4  
#mysql預設utf8mb3，一個字原存成3個byte為了避免中文顯示出現問題，所以設成utf8mb4  
[mysql]  
default-character-set=utf8mb4  
#預設登入設置使用utf8mb4編排資料  
[client]  
default-character-set=utf8mb4  
#預設客戶端設置utf8mb4編排資料  

mysqladmin version -p -S ~/mysqld/mysqlda.sock  
使用在家目錄的sock檔看設定，自己為擁有者，所以不用打密碼(不用-p)  
mysqladmin version -u root -p -h 127.0.0.1 -P 3311  
使用在mysql裡的root(rbean)身分網路查看mysql資訊  
mysqladmin version -p -h 127.0.0.1 -P 3311  
使用在mysql裡的rbean身分網路查看mysql資訊  

**InnoDB 與 MyISAM 檔案儲存方式差異**
MyISAM 資料打包方便、不可進行交易系統(卡住)
InnoDB 可進行交易系統、全部成功或全部失敗

