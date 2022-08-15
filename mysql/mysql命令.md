`show tables;`  顯示此資料庫擁有的table  
`FLUSH PRIVILEGES;`  這是給權限或是消除權限需要另外下的指令    

create database class;  建立class資料庫  
use class  使用class資料庫  
CREATE TABLE t1(    
      id INT,  
      name VARCHAR(100)  
   );  
建立table，資料型態可參考PPT  

DESCRIBE t1;   觀看t1表格的資料型態  
INSERT INTO t1 (id, name)  VALUES(1, '張一');   填入資料到t1，(id, name)可有可無，沒有的話直接按照順序填入資料  
INSERT INTO t1 (name, id) VALUES(2, ‘張三');    這樣也可以  
SELECT * FROM t1;  觀看t1 table  
DROP TABLE t1;  刪除t1 table  
PRIMARY KEY (id)  在創建table時，限制id欄位必須填入值且不能重複  
SELECT * FROM s2 WHERE s2_id between 2 and 4  
SELECT * FROM s2 WHERE s2_id>=2 and s2_id<=4;  找出ID2~4的值  
INSERT INTO Students (id, name)  VALUES(5, '許五'), (6, '許六'), (7, '許七');  一次在Students table中填入多筆資料  
SELECT * FROM Students WHERE id=2;  在Students table中指定觀看id=2的資料  
SELECT * FROM Students WHERE id=5 AND name='許五';  在Students table中指定觀看id=2且name='許五'的資料  
(AND改成OR的話就可以觀看id=2或name='許五'的資料)  

UPDATE Students SET name = "張大明" WHERE id = 1;   更改Students table中id = 1的姓名資料為張大明  
(沒有加入where的話會更改全部姓名資料的名子，會報錯)  

DELETE FROM Students WHERE name = '王二';  刪除Students table中姓名為王二的資料  
DELETE FROM Students WHERE id = 1 OR name = '張大明';  用or可刪除多筆資料，記得設定SET SQL_SAFE_UPDATES=0;  

delete from s2 WHERE s2_birthday like '2002%';   
DELETE FROM s2 WHERE date_format (s2_birthday,'%y')=2002;  
刪除生日日期是2002的人都刪除  
(記得設定SET SQL_SAFE_UPDATES=0; 否則無法刪除多筆資料)  

ALTER TABLE Students ADD COLUMN phone varchar(9);      在Students table中新增phone資料型態為varchar(9)  
ALTER TABLE Students MODIFY COLUMN phone varchar(10);  在Students table中更改phone資料型態為varchar(10)  
ALTER TABLE Students DROP COLUMN phone;                在Students table中捨棄phone這個資料型態  
ALTER TABLE s2 MODIFY COLUMN gender enum('F' , 'M');   在s2 table中的gender資料型態裡只能輸入F跟M  

**注意修改資料型態時，修改前已存在的資料是否有符合，沒有符合的話無法修改**  

SET SQL_SAFE_UPDATES=0;  取消修改保護限制，0改1就可以打開  
(避免正確，但是SQL覺得怪怪的、會刪到很多資料的指令)    

**國家人口資料練習**  
SELECT Name, Population FROM country ORDER BY Population DESC LIMIT 5;    
ORDER BY 排序、DESC 從大到小、LIMIT 5 前五個、人口最多的前 5 個國家  

SELECT Name, Population FROM country ORDER BY Population DESC LIMIT 1 OFFSET 2;  
OFFSET 2 跳過前兩筆資料，人口第 3 多的國家  

SELECT Name, SurfaceArea FROM country ORDER BY SurfaceArea ASC LIMIT 3;  
ASC 由小到大(沒輸入ASC也沒差，ORDER BY預設排列由小到大)，列1出土地面積最小的前 3 個國家  

SELECT Name, Continent, Region FROM country WHERE Continent = 'Asia' AND Region='Eastern Asia' LIMIT 5;  
and 兩個條件的列舉，「或」就使用or，列舉位於 亞洲 東亞 的 5 個國家  

SELECT Name, Continent FROM country WHERE Continent in ('Asia','Antarctica') LIMIT 5;  
兩個條件的列舉，使用WHERE ... in ...，可運用於更多項目的列舉  
(找出位於非洲和北美洲在1918年成立的四個國家)  

SELECT Name, Continent FROM country WHERE  Population < 100;  
大於小於或等於可直接使用符號表示，純數字可以使用 BETWEEN ... AND ...，找出人口數小於 100 國家  

SELECT Name FROM country WHERE Name LIKE 'Ta%';  
使用like 來表示開頭是Ta符合就好，後面隨便，找名稱開頭是 Ta 的國家  

SELECT Continent FROM country GROUP BY Continent;  
把國家資料以大陸板塊為單位加進群組(group by)來表示或是使用  
SELECT DISTINCT Continent FROM country;  
DISTINCT不重複顯示，找出地球上有哪幾個大陸？  

SELECT Continent, COUNT(*) FROM country GROUP BY Continent;  
以大陸板塊為單位查詢國家數目  

SELECT Continent, AVG(Population), SUM(Population), MAX(Population), MIN(Population) AS pop_min FROM country GROUP BY Continent;  
每個大陸上的國家 平均、總、最大、最小人口數？  

...(欄位) as ...(自訂名稱) 欄位名稱變成自己自訂的  
