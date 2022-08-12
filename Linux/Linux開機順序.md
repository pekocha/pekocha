**vmlinuz**
==
vmlinuz 是LINUX 核心名稱  
BIOS儲存於BIOS ROM晶片  
EFI & UEFI 新版的BIOS介面  
`[ -d /sys/firmware/efi ] && echo UEFI || echo BIOS`  
確認是UEFI還是BIOS  
在 Windows 10 => 打開 CMD 或 Windows + R 快捷打開執行 => 輸入 msinfo32  

sudo gdisk /dev/sda -l  
確認16*4Bytes的磁區分割表是MBR or GPT  
在 Windows 10 => Windows 鍵 + X => 點選磁碟管理  
對磁碟0 或 磁碟1 右鍵選內容 => 頁籤選磁碟區  

**開機流程 - BIOS**
==
1.按下開機鍵  
2.BIOS 執行執行開機自我測試（Power-on Self Test，POST）  
(檢查CPU、記憶體、硬碟...是否正常，正常會叫一聲)  

**開機流程 - MBR**
==  
3.讀取第一個可開機裝置的 MBR  
(可能是硬碟、USB、光碟)  
4.啟動 MBR 中的 Boot Loader  

**開機流程 - Boot Loader**
==
5.提供開機選單  
(如果有多個作業系統的話)  
6.Chain loading  
（控制權轉交給其他 loader，因為檔案太小不能做太多事）  
之後做以下三件事  
(1)將 Linux 核心及 initramfs = initrd 載入到記憶體中(載入就是解壓縮)  
(2)將 initramfs 位址傳給 Kernel  
(3)將控制權交給 Kernel  

**開機流程 - Kernel**
==
7.利用initramfs 位址掛載臨時的檔案系統initramfs，之後載入驅動程式來跟硬體裝置做溝通  
8.檢測裝置是否正常  
9.之後執行systemd程式    /sbin/init -> /lib/systemd/systemd  
  第一隻程式所以PID是1   









