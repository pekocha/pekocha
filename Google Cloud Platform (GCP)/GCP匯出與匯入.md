**GCP匯出ubuntu載入到VAWARE**
==
1.設定可以ssh連線、帳號設置密碼、叢集裡面的apline也要  
2.硬碟轉成影像檔  
3.匯出影像檔(vmdk檔)  
4.放到cloud storage，要錢，名子全世界不能重複  
5.匯出(建立甚麼機器，GOOGLE就用什麼機器幫你匯出)  
6.在cloud storage下載  
7.在vaware建立一個一樣的環境後，把下載的檔案覆蓋掉硬碟檔  
8.vmware tools 一定要記得裝  
9.設定裡打勾硬體輔助虛擬化，才能用KVM進去ALPINE  

**從VAWARE匯出KVM到GCP**
==
1.先CD前往目標資料夾  
2.qemu-img convert -f qcow2 disk/alpine.qcow2 -O vmdk disk/alpine.vmdk  
-O指定匯出vmdk檔為alpine.vmdk  
3.scp katana1791@192.168.61.19:~/wk/disk/alpine.vmdk .  
輸入想要從哪裡下載東西  
4.在cloud storage上傳檔案  
5.建立映像檔，來源:虛擬硬碟，在虛擬硬碟檔案處選擇剛剛上傳的  
6.建立VM執行個體，選擇ubuntu系統，開機磁碟使用自訂映像檔後建立  
7.連線開機(之前要設定可以root連線或是創建別的帳號)  
