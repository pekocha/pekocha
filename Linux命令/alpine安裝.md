
建立 Alpine 虛擬主機   
-------------------------------------------
**1. 下載 Alpine 光碟檔**   
https://alpinelinux.org/downloads/    

選擇 Virtual 版本, 型別為 x86_64 (alpine-virt-3.15.1-x86_64.iso)    

[註] Similar to standard. Slimmed down kernel. Optimized for virtual systems    

**2. 啟動 VMware Workstation Player, 建立 alp.dt 虛擬主機**

 **A.** 請選擇 "I will install the operating system later", 開始建立 alp.dt 虛擬主機   
 **B.** 作業系統選擇 Linux, 版本為 Other Linux 5.x kernel 64-bit    
 **C.** Virtual Machine name 設為 alp.dt, Location 設為 c:\alp.dt   
 **D.** Maximum disk size (GB): 800, 點選 "Store virtual disk as a single file"   
 **E.** 點選 Customize Hardware 按鈕, 移除 Printer, Sound Card, USB Controller,     
    然後設定 New CD/DVD(IDE), 點選 Use ISO Image File, 選擇 alpine-virt-3.15.1-x86_64.iso,    
    點選 Processors, 勾選 Virtualize Intel VT-x/EPT or AMD-V/RVI    
 **F.** 啟動 alp.dt 虛擬主機       


Alpine 硬碟安裝   
--------------------------------------------
**1. 登入 Alpine 虛擬主機**     
localhost login: root     
Welcome to Alpine!      

The Alpine Wiki contains a large amount of how-to guides and general     
information about administrating Alpine systems.     
See <http://wiki.alpinelinux.org/>.     

You can setup the system with the command: setup-alpine    

You may change this message by editing /etc/motd.    
localhost:~#     

**2. 開始安裝**    
localhost:~# setup-alpine    
Available keyboard layouts:    
af     be     cn     fi     hu     it     lk     mm     pl     sy     uz    
al     bg     cz     fo     id     jp     lt     mt     pt     th     vn    
am     br     de     fr     ie     ke     lv     my     ro     tj    
ara    brai   dk     gb     il     kg     ma     ng     rs     tm    
at     by     dz     ge     in     kr     md     nl     ru     tr    
az     ca     ee     gh     iq     kz     me     no     se     tw    
ba     ch     epo    gr     ir     la     mk     ph     si     ua    
bd     cm     es     hr     is     latam  ml     pk     sk     us     
Select keyboard layout [none]: us      
Select variant []: us    
 * Caching service dependencies ...     
 [ ok ]      
 * Setting keymap ...     
 [ ok ]     
Enter system hostname (short form, e.g. 'foo') [localhost]: alp.dt     
Available interfaces are: eth0.     
Enter '?' for help on bridges, bonding and vlans.      
Which one do you want to initialize? (or '?' or 'done') [eth0]      
Ip address for eth0? (or 'dhcp', 'none', '?') [dhcp]  
Do you want to do any manual network configuration? [no]   
udhcpc: started, v1.31.1  
udhcpc: sending discover  
udhcpc: sending discover  
udhcpc: sending select for 10.0.2.15  
udhcpc: lease of 10.0.2.15 obtained, lease time 86400  

Changing password for root  
New password: root   
passwd: password for root changed by root   

Which timezone are you in? ('?' for list) [UTC] Asia   
What sub-timezone of 'Asia' are you in? ('?' for list) Taipei    
 * Starting busybox acpid ...   
 [ ok ]   
 * Starting busybox crond ...   
 [ ok ]    

HTTP/FTP proxy URL? (e.g. 'http://proxy:8080', or 'none') [none]   
Which NTP client to run? ('busybox', 'openntpd', 'chrony' or 'none') [chrony]  
 * service chronyd added to runlevel default    
 * Caching service dependencies ...   
 [ ok ]   
 * Starting chronyd ...    
 [ ok ]    

Available mirrors:    
1) dl-cdn.alpinelinux.org   
2) uk.alpinelinux.org   
3) dl-2.alpinelinux.org   
4) dl-4.alpinelinux.org   
5) dl-5.alpinelinux.org   
6) dl-8.alpinelinux.org  
7) mirror.yandex.ru  
8) mirrors.gigenet.com  
9) mirror1.hs-esslingen.de  
.............   

r) Add random from the above list   
f) Detect and add fastest mirror from above list   
e) Edit /etc/apk/repositories with text editor   

Enter mirror number (1-46) or URL to add (or r/f/e/done) [1]: 6   
Added mirror dl-8.alpinelinux.org   
Updating repository indexes... done.   
Which SSH server? ('openssh', 'dropbear' or 'none') [openssh]    
 * service sshd added to runlevel default  
 * Caching service dependencies ...  
 [ ok ]   
ssh-keygen: generating new host keys: RSA DSA ECDSA ED25519     
 * Starting sshd ...  
 [ ok ]  
Available disks are:  
  sda	(536.9 GB ATA      QEMU HARDDISK   )  
Which disk(s) would you like to use? (or '?' for help or 'none') [none] sda  
The following disk is selected:  
  sda	(536.9 GB ATA      QEMU HARDDISK   )  
How would you like to use it? ('sys', 'data', 'lvm' or '?' for help) [?] sys  
WARNING: The following disk(s) will be erased:  
  sda	(536.9 GB ATA      QEMU HARDDISK   )  
WARNING: Erase the above disk(s) and continue? [y/N]: y  
Creating file systems...  
Installing system on /dev/sda3:  
/mnt/boot is device /dev/sda1  
100% ############################################==> initramfs: creating /boot/initramfs-virt    
/boot is device /dev/sda1    

Installation is complete. Please reboot.    

alp:~# poweroff   


**3. 再次啟動 VMware Workstation Player, 移除 CD/DVD 裝置, 然後啟動 alp.dt 虛擬主機,  
登入 Alpine 虛擬主機**  

alp.dt login: root  
Password: 按 Enter  
