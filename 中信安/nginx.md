# NGINX 靜態 Web 服務部署(阿助)

學習如何使用 NGINX 架設託管靜態網頁的 Web 服務

## 要求

* [ ] 使用 `yum` 命令安裝 `nginx` 服務

```終端輸入/輸出
1.yum install nginx
```

* [ ] 新增 `www` 使用者並設定 `GID` 、 `UID` 為 `501` ，並將 `nginx` 服務啟動的 `user` 、 `group` 修改為 `www` 使用者。

```終端輸入/輸出
1.groupadd -g 501 www
增加www的群組並設定gid為501
2.adduser www -u 501 -g 501
增加使用者www並設定pid、gid為501
3.passwd www
給密碼
4.nano /etc/nginx/nginx.conf
5.把 user nginx; 改成 user www www;
指定服務啟動的user與group
6.ps -aux | grep "nginx"
檢查是否更改成功
(systemctl enable nginx)
```

* [ ] 在Yum安裝的 `nginx.conf` 中引入 `/opt/vhost` 資料夾下的虛擬站台相關設定

```終端輸入/輸出
1.include /opt/vhost/web.conf;

```

* [ ] 在 `/opt/vhost` 下建立名稱 `web.conf` 的虛擬站台設定，站台要求如下（配置參閱Yum安裝的`nginx.conf`）:
    + 站台配置端口 `80`
    + 站台配置名稱 `本機IP`
    + 站台預設文件路徑 `/opt/web`
    + 站台預設首頁名稱 `index.html` 設定首頁內容為 `Test Web Page`
    + 站台 access log 存放路徑 `/opt/logs/nginx/web_access.log`
    + 站台 error log 存放路徑 `/opt/logs/nginx/web_error.log`

```終端輸入/輸出
1.firewall-cmd --zone=public --permanent --add-service=http
默認CentOS7 使用的防火牆firewalld 是關閉http 服務的（打開80 端口）

2.firewall-cmd --reload

3.setsebool -P httpd_can_network_connect on
SELinux 阻擋連線，要把設定打開

4.mkdir -p  /opt/logs/nginx/
創建資料夾

5.touch /opt/logs/nginx/web_error.log
創建錯誤log檔

6.touch /opt/logs/nginx/web_access.log
創建操作log檔

7.mkdir /opt/vhost
創建vhost資料夾

8.cp /etc/nginx/nginx.conf /opt/vhost/web.conf
複製原本的設定檔做修改

9.mkdir /opt/web

10.nano /opt/web/index.html
輸入<h1>Test Web Page</h1>
```

* [ ] 在 `/opt/vhost` 下建立名稱 `web_ssl.conf` 的虛擬站台設定，站台要求如下（配置參閱Yum安裝的`nginx.conf`）:
    + 站台配置端口 `443` 
    + 站台配置名稱 `本機IP`
    + 站台設定加密連線，使用自簽憑證
    + 站台預設文件路徑 `/opt/web_ssl`
    + 站台預設首頁名稱 `index.html` 設定首頁內容為 `Test Web SSL Page`
    + 站台 access log 存放路徑 `/opt/logs/nginx/web_ssl_access.log`
    + 站台 error log 存放路徑 `/opt/logs/nginx/web_ssl_error.log`

```終端輸入/輸出
1.cp /etc/nginx/nginx.conf /opt/vhost/web_ssl.conf
複製設定檔修改

2.touch /opt/logs/nginx/web_ssl_access.log
創建操作log檔

3.touch /opt/logs/nginx/web_ssl_error.log
創建錯誤log檔

4.mkdir /opt/web_ssl

5.nano /opt/web_ssl/index.html
輸入<h1>Test Web SSL Page</h1>

6.mkdir /etc/nginx/ssl
建立一個放置憑證的目錄

7.openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/nginx/ssl/nginx.key -out /etc/nginx/ssl/nginx.crt

req：使用 X.509 Certificate Signing Request（CSR） Management 產生憑證。
-x509：建立自行簽署的憑證。
-nodes：不要使用密碼保護，因為這個憑證是 NGINX 伺服器要使用的，如果設定密碼的話，會讓伺服器每次在啟動時書需要輸入密碼。
-days 365：設定憑證的使用期限，單位是天，如果不想時常重新產生憑證，可以設長一點。
-newkey rsa:2048：同時產生新的 RSA 2048 位元的金鑰。
-keyout：設定金鑰儲存的位置。
-out：設定憑證儲存的位置。

8.firewall-cmd --zone=public --permanent --add-service=https
開啟https 403 端口

9.firewall-cmd --reload

10.netstat -ntpl 
查看端口
```

* [ ] 請列出以下相關指令：
    + 檢查 `nginx` 設定檔：
    + 啟動 `nginx`：
    + 停止 `nginx`：
    + 重新載入 `nginx` 設定檔：
```
chkconfig nginx
systemctl start nginx
systemctl stop nginx
systemctl reload nginx
```
---
## 额外项目

* [ ] 從系統指令顯示Nginx版本號

```終端輸入/輸出
nginx -V
```

* [ ] 查詢Http狀態碼 200、301、302、304、401、403、404、500、502、504 各自代表意義

```答案
200 OK
請求已成功，請求所希望的響應頭或數據體將隨此響應返回

301 Moved Permanently
被請求的資源已永久移動到新位置，並且將來任何對此資源的引用都應該使用本響應返回的若干個URI之一。

302 Found
要求客戶端執行臨時重定向（原始描述短語為“Moved Temporarily”）。[19]由於這樣的重定向是臨時的，客戶端應當繼續向原有地址發送以後的請求。只有在Cache-Control或Expires中進行了指定的情況下，這個響應才是可緩存的。

304 Not Modified
表示資源在由請求頭中的If-Modified-Since或If-None-Match參數指定的這一版本之後，未曾被修改。在這種情況下，由於客戶端仍然具有以前下載的副本，因此不需要重新傳輸資源。

401 Unauthorized
類似於403 Forbidden，401語意即「未認證」，即使用者沒有必要的憑據。[31]該狀態碼表示當前請求需要使用者驗證。

403 Forbidden
伺服器已經理解請求，但是拒絕執行它。與401回應不同的是，身分驗證並不能提供任何幫助，而且這個請求也不應該被重複提交。

404 Not Found
請求失敗，請求所希望得到的資源未被在伺服器上發現，但允許使用者的後續請求。[34]沒有資訊能夠告訴使用者這個狀況到底是暫時的還是永久的。

500 Internal Server Error
通用錯誤訊息，伺服器遇到了一個未曾預料的狀況，導致了它無法完成對請求的處理。沒有給出具體錯誤資訊。

502 Bad Gateway
作為閘道器或者代理工作的伺服器嘗試執行請求時，從上游伺服器接收到無效的回應。

504 Gateway Timeout
作為閘道器或者代理工作的伺服器嘗試執行請求時，未能及時從上游伺服器（URI標識出的伺服器，例如HTTP、FTP、LDAP）或者輔助伺服器（例如DNS）收到回應。
```
