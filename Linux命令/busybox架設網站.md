**busybox**
==
1.```sudo busybox httpd -p 80 -h ./myweb```  
架設myweb資料夾的index.html檔案到通路80上面  

2.```ps aux | grep httpd```   
查詢自己架設網站的代號  

3.舉例   
```
root@apt-3:/home/katana1791# ps aux | grep httpd   
root        1066  0.0  0.0   3316   112 ?        Ss   03:04   0:00 busybox httpd -p 80 -h ./webroot   
root        2207  0.0  0.4   8168  2540 pts/1    S+   04:46   0:00 grep --color=auto httpd    
```

4.```sudo kill -9 1066```(代號)  
下架網站，代號可透或查詢得知  
