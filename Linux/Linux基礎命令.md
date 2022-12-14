**基礎指令**
==
 ```ls```  目錄清單  
 ```ls -al```  目錄清單，包含隱藏目錄  
 ```echo ~```  家目錄的路徑  
 ```pwd```   目前所在的工作目錄  
 ```cd /```   前往根目錄  
 ```echo "HELLO $USER"```   單引號只是單純的字串，雙引號可把命令讀出來  
who指令 -l(清單)-H(標題)-m(當前使用者)-q(簡易顯示)     
 ```su ybean(帳號)```   切換帳號  
 ```sudo nano /etc/sudoers```  更改權限帳號  
 ```%myring ALL=(ALL:ALL) NOPASSWD:ALL```   把在myring資料夾的帳號設成有SUDO權限而且免密碼  
 ```sudo timedatectl set-timezone Asia/Taipei```   更改時區(台灣)  
 ```chmod +x ./mysh.sh```  增加mysh.sh檔案的可執行權限(全部人)   
**(檔案權限RWX分別代表4、2、1，例如 chmod 744 test.ing 代表自己權限最高，其他人只有R權限)**     
 ```sudo chown rbean testing/```  改變tesiting資料夾的使用者變成rbean   
`free -mh` 檢視電腦記憶體，-mh人性化檢視  
`fmt -u` 格式化，減少空格調整格式  
`df` 檢視硬碟資訊  
`read -t5` 在五秒內輸入數字  
`read -n2` 只能輸入2個字元，輸入2字元後自動輸出  
`ping -c 4 -w 1` 回應4筆就好，超過1秒就不要了  
`((數字+數字)) $((變數+數字))`  可做數學運算
`$0$1$2$3$4` $0是執行程式本身，其他是在執行程式時後面附加上去才會套入內容的變數
`pw=%(cat word)` 變數等於別的文字本身，可利用於密碼  
PATH=$PATH:~ 設置家目錄在系統路徑裡(最後面)  
PATH=~:$PATH 設置家目錄在系統路徑裡(最前面)  
[ "$USER" != "root" ] && exit  不是ROOT或是SUDO身分的話就無法執行程式  
read -s 不顯示輸入的值  
read -e 輸入時按兩下tab鍵的話會幫你顯示相關檔案  
echo "aaaaa" |tee txt  新內容aaaaa覆蓋過去txt檔案  
echo "bbbbb" |tee -a txt  不覆蓋在後面添加  
yes 一直不斷丟出y  
sudo shutdown -h now 馬上關機
**NANO文字編輯指令**
alt shift 3  顯示行數  
ctrl + /  移動到想去的行數，例如:492  

echo -e "rbean\nrbean" | sudo adduser -s /bin/bash rbean  echo密碼兩次、並\n換行給新創的帳號rbean，rbean使用bash的貝殼程式  
tty 可以查詢目前自己連線的終端機是第幾台，第一台是/dev/pts/0，在本機輸入會變成tty1

**grep**
==
`grep ^0.0.0.0` 抓取這一行的開頭的0.0.0.0  
`grep -f 檔案 /etc/passwd`      在/etc/passwd裡面grep出檔案裡面的內容  
`grep -c -f 檔案 /etc/passwd`   在/etc/passwd裡面grep出檔案裡面的內容，並告知幾筆  
`grep -w JONE` 找尋完整單字JONE  
`grep ^%` 抓空白列  
`grep "a3a$"` 從尾端找a3a  
`grep ^asd$`  找尋完全一樣的asd  
`file 檔案` 可看單個檔案的屬性  

**帳號管理(ubuntu)**
==
創帳號: sudo useradd -m(給家目錄) -s(豐富的貝殼程式可以用) /bin/bash ybean(帳號名稱ybean) **bash權限較高，sh權限較低**  
創密碼: sudo passwd ybean(密碼為ybean)  
創群組: sudo groupadd sudoagent(名稱sudoagent)  
查看是否創建成功: cat /etc/group  
加群組: sudo usermod -a -G sudoagent ybean(名稱ybean)  
刪帳號: sudo userdel -r(-r連同根目錄) ybean(名稱ybean)  
查詢線上人數與pts: who  
把人踢下線: sudo pkill -kill -t  pts/1(用who指令查詢該帳號的pts為多少)  
鎖密碼:sudo usermod -L ybean(帳號名)  
解鎖密碼:sudo usermod -U ybean(帳號名)  

echo boss:bbbb |sudo chpasswd  
快速更改密碼，例:更改boss的密碼為bbbb  

sudo chpasswd < pwlist  
直接用pwlist內的內容導入進去chpasswd裡面的參數(一堆密碼，餵給他)  

**SCP指令**
==
1.從WINDOS傳檔案到模擬機 (透過WIN)  
scp ABC.txt(檔案) tasuke@192.168.85.19:/home/tasuke/C.txt(要改檔名的話可以改名子，不填入就一樣)  
2.從模擬機傳檔案到WINDOS(透過WIN)  
scp tasuke@192.168.85.19:/home/tasuke/ABC.zip ./HELLO.zip(要改檔名的話可以改名子，不填入就一樣)  
3.從模擬機傳檔案到另一台模擬機  
scp ./ABC.zip tasuke@192.168.85.24:/home/tasuke/(要改檔名的話可以改名子，不填入就一樣)  
scp katana1791@35.234.58.75:/home/katana1791/c.txt ./ 把c.txt傳回本機目前的位子(./ 代表目前位子)    

**公私鑰發放**
==
發公鑰跟私鑰在自己的家目錄裡面的.ssh ```ssh-keygen -t rsa -P ''```   
把公鑰給tasuke02 ```ssh-copy-id tasuke@192.168.85.24```  
編輯hosts檔連結IP位子跟名稱  ```sudo nano /etc/hosts```
不登入主機查看資料 ```ssh tasuke@192.168.85.24 -p 22 ls -al```   
(ssh本來就走22 port，不加沒差)

**source、export**
==
source allfun 跟 .「空一格」allfun一樣 allfun為檔案名稱  
把另一個檔案內的資料搬過來使用  

export kk=kkkkkk 可以把指定的變數往下繼承(可配合source命令)  
在提示號使用時可下傳到每個程式，除非在程式內使用export在往下蓋，  
但一離開程式，則命令回歸到在提示號下過的(最上層)  

**ssh連線設定**
==
sudo nano /etc/ssh/sshd_config  
找到 PasswordAuthentication 改成 yes  
sudo systemctl stop sshd  
sudo systemctl start sshd  

