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


**SQL Constraints 限制、約束**
==
PRIMARY KEY = NOT NULL (不能是空值) + UNIQUE (不能與他人重複)  
