**ubuntu設定**
==
`sudo passwd` 進入虛擬機後先設定自己(google的帳號)的密碼跟root的密碼   
`sudo apt-get update`  
`sudo apt-get upgrade`  
`sudo reboot` 重啟更新密碼與資訊  
`sudo nano /etc/ssh/sshd_config`  
`PasswordAuthentication no` 把no改成yes，允許密碼登錄  
`#GatewayPorts no` 改成 GatewayPorts yes 允許ssh建立其他port  
`sudo systemctl restart sshd.service` 重啟ssh服務  
`sudo apt install net-tools` 安裝網路工具  
`sudo useradd -m -s /bin/bash bigred` 創造bigred  
`sudo useradd -m -s /bin/bash rbean`  創造rbean  
(之後設定密碼跟sudo群組)  

**架網站到公有IP(GCP)上並且有分頁**
==
1.用指令把資料分析的結果輸出到文件上，.csv或是.txt  
2.把檔案傳輸到桌面上用excel或是word進行編輯或表格化  
3.用excel的話增加工作表就等於在網頁上多增加一個頁面，例如  
概覽  
雲林縣各鄉鎮市快篩藥局數量  
雲林縣藥局地址與快篩試劑數量  
4.另存輸出檔案類型記得為html擋並存於資料夾中，檔名為index.html網頁才讀的到檔案  
5.把資料夾進行zip壓縮運用scp上傳於虛擬機  
6.把zip檔解壓縮後使用busybox httpd -p 80 -h ./(資料夾名稱) 把網站放上網路  
7.記得上GCP機器編輯把Allow HTTP traffic跟Allow HTTPS traffic打勾  
8.想刪除網路時使用ps aux | grep httpd 查詢自己架設網站的代號 (搜尋關鍵字httpd的命令)  

root@apt-3:/home/katana1791# ps aux | grep httpd  
root        1066  0.0  0.0   3316   112 ?        Ss   03:04   0:00 busybox httpd -p 80 -h ./webroot  
root        2207  0.0  0.4   8168  2540 pts/1    S+   04:46   0:00 grep --color=auto httpd  

8.sudo kill -9 1066(代號)  下架網站，代號可透或查詢得知  

**使用GCP開啟其他port**
==
1.虛擬私有雲網路>防火牆>建立防火牆規則  
2.名稱allow-http-(有8080、8888...)  
3.目標標記打上http-server  
4.來源ipv4範圍打上0.0.0.0/0  
5.tcp上打上想要連接上的port，配合第2點  
6.記得Allow HTTP traffic跟Allow HTTPS traffic一樣要打勾  
7.不想要開80port的話再去防火牆那邊刪掉即可  
