＊＊Alpind虛擬機＊＊
＝＝
apk update
apk upgrade
apk add tree nano sudo unzip zip wget grep bash curl
tree /home 確定指令是否安裝成功
adduser -s /bin/bash(可使用bash) -h /home/bigred(有家目錄) -D bigred(產生帳號) 辦帳號
addgroup bigred wheel 把帳號加入wheel群組(SUDO權限)
passwd bigred (給密碼，可能會說密碼太短太簡單，可忽略)
進入nano /etc/suduers 找到# %wheel ALL=(ALL) NOPASSWD: ALL 前的#刪除加入wheel群的人就有SUDO權限且免密碼
sudo usermod -dl root 把root帳號停止使用後reboot重開機後使用SUDO帳號操作(root帳號容易被駭客入侵)
sudo nano /etc/network/interfaces 設定固定網路IP位子，PING時注意防火牆

auto lo
iface lo inet loopback

auto eth0
#iface eth0 inet dhcp
iface eth0 inet static
        address 192.168.85.39
        netmask 255.255.255.0
        gateway 192.168.85.2

sudo nano /etc/sysctl.conf 到此路徑
輸入net.ipv6.conf.all.disable_ipv6=1 停用ipv6網路段
輸入sudo /etc/init.d/sysctl restart  重啟網路
sudo /etc/init.d/sysctl restart

*前面可以先做允許ROOT用WINDOWS做ssh連線(字比較大)*
sudo nano /etc/ssh/sshd_config
PermitRootLogin yes
sudo service sshd restart

到sudo nano /etc/ssh/ssh_config
把StrictHostKeyChecking ask 改成StrictHostKeyChecking no 
(第一次連線沒公鑰的話會自動接收，yes的話要自己輸入yes)

編輯登入畫面沒有支援cowsay等等的套件，但可透過複製貼上後cat指令使用，但需注意$USER指令
sudo nano /etc/profile 簡化命令，例如alias cls='clear' 
虛擬機間免密碼登入，參考【5/11】的筆記
