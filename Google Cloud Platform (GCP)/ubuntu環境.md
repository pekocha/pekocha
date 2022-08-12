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
