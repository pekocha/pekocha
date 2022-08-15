**為什麼要用資料庫?**
==
由於傳統的資料儲存方式存在很多弊端，因此要用資料庫的方式來整合資料  
正規化資料庫分為主表跟關聯表  

**ER-MODEL的關聯**
== 
(mysql ppt1)  
長方形資料表實體  
橢圓形資料表屬性  
菱形資料表關聯  
各個資料之間使用線條連接  

**鳥爪圖**  
O    = 0，沒有  
|    = 1，至少1  
鳥爪 = 很多  

**資料庫組成**
==
1.Flied一個欄位  
2.Record很多欄位組成一筆資料  
3.Table很多比資料組成一個表  
4.Database很多張表組成一個資料庫  
**Schema 表頭、欄位名稱屬性，描述資料的資料，資料屬於文字型態或是數字型態**  

**SQL:結構化查詢語言**
==
雖然大家依照ANSI SQL Standard 下去開發語言  
但還是大家還是有些許的不同，總共分成三種類型  
T-SQL(Transact-SQL，例如Microsoft SQL Server跟Sybase SQL Server )  
PL/SQL(Procedural Language/SQL，例如Oracle, MySQL, PostgreSQL)  
SQL PL(例如IBM DB2)  

**MySQL 和 MariaDB 的關聯性**
==
MySQL 原為開源（open source）的關聯式資料庫，被收購後現分成  
 Community (免費)及 Enterprise (要錢，適合企業使用，提供困難解決的服務)  
兩個版本。MariaDB 由原開發者公司之後出來開發強調免費、開源  
跟原本的MySQL相似且優化  

**SQL的語法**
==
DDL 定義資料Schema裡的語法  
DQL 查詢資料的語法  
DML 操作資料的語法  
DCL 控制資料庫權限的語法，使用者讀寫看的規則  

**資料庫引擎:innoDB**
==
Table Lock（只要有使用者新增或刪除某筆特地的資料，整個Table會被鎖住，其他使用者無法操作，等新增結束才可修改）  
Record Lock（指鎖定一筆資料，在大量新增資料時，可以只鎖定正在新增的資料，其他使用者仍可查詢其他資料）  
MySQL 5.5 版本後，InnoDB為預設儲存系統，  
InnoDB支援Record Lock 相較於Table Lock鎖定多筆資料，  
Record lock可只鎖定單筆資料，因此可提高資料處理效率，  
也可避免大量寫入造成無法讀取資料的問題  

**InnoDB的Transaction四原則**
==
A (Atomicity): 交易只有完全成功或完全失敗  
C (Consistency): 確保交易前後資料庫資料狀態一致  
I (Isolation): 確保交易過程中是1對1  
D (Durability): 確保交易完成後的數據修改有保留  


**MYSQL constraint 限制、約束**
==
NOT NULL - 不能為空值  
UNIQUE - 不可與其他值相同  
PRIMARY KEY - 不可為空值且不可與其他值相同  
FOREIGN KEY - 連接至別的table的PRIMARY KEY  
CHECK - 限制，例如大於小於等等  
DEFAULT - 在某個資料型態設置一個值，在輸入資料時，此資料型態沒被輸入值的時候，  
          自動代入DEFAULT設置好的值，但仍可輸入null維持空值(小灰null)  
CREATE INDEX - 把資料型態放進記憶體，運用二元樹 (Binary tree)運算加快搜尋，最好唯一值像是PRIMARY KEY  

**constraint NOT NULL、NULL**  
沒設定NOT NULL的話，就會預設NULL  

**constraint PRIMARY KEY**  
show create table (table名稱);  
可以看當初創建table時的資訊  
分辨哪個是primary key、哪些是NOT NULL + UNIQUE  

一個table只能有一個primary key  
primary key(ID) 或是 primary key(ID,Lastname)  
ID跟Lastname的組合為唯一這樣  
那個欄位的值不跟其他欄位重複而且不能為空值  

**constraint FOREIGN KEY**  
FOREIGN KEY (PersonID) REFERENCES Persons1(ID)  
本身資料型態PersonID連接到Persons1的primary key的ID  

**constraint FOREIGN KEY刪除方式**  
1.用show create table去找CONSTRAINT的名稱  
'Orders', 'CREATE TABLE `Orders` (\n  `OrderID` int(11) NOT NULL,\n  `OrderNumber` int(11) NOT NULL,\n  `PersonID` int(11) DEFAULT NULL,\n  PRIMARY KEY (`OrderID`),\n  KEY `PersonID` (`PersonID`),\n  CONSTRAINT `Orders_ibfk_1` FOREIGN KEY (`PersonID`) REFERENCES `Persons2` (`ID`)\n) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4'
2.輸入ALTER TABLE drop foregin key Orders_ibfk_1(找到的名稱);  

**constraint cheak**  
ALTER TABLE Orders add constraint cheak (OrderNumber>=10);  
增加資料型態限制OrderNumber>=10到Orders的表格裡面  

**constraint DEFAULT**  
City varchar(255) DEFAULT 'Taiwan'  
增加DEFAULT，沒填入資料的話就會自動填入Taiwan  
但在輸入資料時一樣可以填null進去(小灰null)  

