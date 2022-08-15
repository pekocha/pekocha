**Write Once Run Anywhere - Java**
==
寫過一次程式，在其他作業系統環境都可以執行  
今天客戶要從linux換到windows server也完全沒問題  
一種漫遊的概念  

**Java為什麼能做到呢?**  
我們寫的Java程式副檔名為.java，  
經過編譯器會產生副檔名為.class的機械碼，  
Java機械碼只給Java自己設計的機器來讀  
（Java的Virtul Machine，簡稱JVM ），  
Java在所有系統都有JVM，所以能夠在所有作業系統都可執行，  
例如JVM在Windows及Linux作業系統皆用C語言  
（但程式碼結構不一樣）  

java語言可用來開發`Hive,Zeppelin,Spark,Hadoop`  
linux:libjvm.so  
windows:jvm.dll  

**java程式機械碼**  
前四碼一定是CA FE BA BE  
(咖啡小寶貝)  
