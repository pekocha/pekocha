**read and REPLY**
==
`read` 之後可以輸入一個詞讓電腦記  
`echo $REPLY` 回復剛剛讓電腦記的詞  
`[ "$REPLY" = "1" ];echo $?` 判斷句，正確=0，錯誤=1  
`[ "$ans" == "aaa" ] && echo ok` 如果變數ans=aaa回覆aaa  
`read -p "choice?" ans` 產生choice?字串，輸入的值變成變數ans  

**echo**
==
`echo -e "123\n456\n"` -e處理特殊字元，遇到\n等於換行  
`ABC=123 ; unset ABC` 解除變數  
`echo 123>123.txt` 建立123.txt檔，內容123  
`echo 123>>123.txt` 內容除了原本的，增加123  
`name="tasuke's home" 等於 name=tasuke\'s\ home` 利用\跳脫符號，echo出來是一樣的  
`echo $?` 詢問上一個程式是否成功，成功=0、失敗=1    

**更改貝殼程式**
==
mkdir -p base/{a,b,c}   只有sh的貝殼程式會創建失敗  
變成單一個資料夾，名稱為{a,b,c}，而不是分別的資料夾a、b、c  

更改貝殼程式，來/etc/passwd用nano更改，登出後登入就生效  

**判斷句式**
==
`[ ! -d mybanana ] && mkdir mybanana`  如果mybanana資料夾不存在的話，創建一個同名資料夾  
`[ ! -f mybanana.sh ] && touch mybanana.sh` 
如果mybanana.sh不存在的話，創建一個同名檔案，>dev\null 把執行過程正缺輸出或是錯誤輸出都丟到黑洞不顯示

**可輸入多重答案，配合多個結果**
==
read -p "number?" ans  
case $ans in  
1)  
echo "1" (;;也可以在這行)  
;;  
2)  
echo "2"(;;也可以在這行)  
;;  
*)  
echo "other"  

esac  

**迴圈程式**
==
for ans in a b c d   
do  
echo $ans  
sleep 1  
done  

for ip in 1 2 3 或是 for ip in `seq 1 3`   
do  
done  


**迴圈程式(參數寫法)**  
for ans in $1 $2 $3 $4 或是for ans in $@ $* 可以在執行程式時輸入幾個就有幾個  
do  
echo $ans  
sleep 1  
done  
echo $0  
echo $*  
echo $#  
在執行程式時才把變數帶進去  
例如:./a.sh AAA BBB CCC DDD  
$0 是程式本身  
$* 列出全部變數  

**迴圈程式2**  
for ((n=1;n<=4;n=n+1)) 起始值;限制值;累加值  
do  
echo $n  
done  
echo end  

**無限程式**
==
答出正確答案才停  
while true   (while true也寫成while:)  
do  

break  
  
done  

答出正確答案1才停，可加continue，可套入if問句程式或是  
多重答案程式  

shift 踢掉$1的變數，後面的變數替補上去
$# 算出總共幾個變數  

**無限程式4圈**  
#!/bin/bash   
w=11  
while (($w<=15))  
do  
echo $w'>>>>'  
 x=3  
 while (($x<=5))  
 do  
 echo ''$x'>'  
  y=6  
  while (($y<=8))  
  do  
  echo -n $y':'  
   z=9  
   while (($z <= 13))  
   do  
   echo -n "$z"' '  
   z=$((z+1))  
   done  
   echo  
  y=$((y+1))  
  done  
 x=$((x+1))  
 done  
w=$((w+1))  
done  

**無限程式4圈(參數寫法)**   
#!/bin/bash  
echo -n "請輸入第1段區間(輸入2組數字): "; read w1 w2  
echo -n "請輸入第1段區間(輸入2組數字): "; read x1 x2  
echo -n "請輸入第1段區間(輸入2組數字): "; read y1 y2  
echo -n "請輸入第1段區間(輸入2組數字): "; read z1 z2  
w=$w1  
while (($w<=$w2))  
do  
  echo "$w>>>>"  
  w=$(($w+1))  
  x=$x1  
  while (($x<=$x2))  
  do  
    echo " $x>"  
    x=$(($x+1))  
    y=$y1  
    while (($y<=$y2))  
    do  
      echo -n "  $y:"  
      z=$z1  
      while (($z<=$z2))  
      do  
        echo -n "$z "  
        z=$(($z+1))  
      done  
      y=$(($y+1))  
      echo  
    done  
  done  
  echo  
done   

**設定變數、函數**
==
ans="1 2 3 4"  
set -- $ans  
可以把1 2 3 4設成$1$2$3$4  

**整數變數運算**  
Declare -i a  
宣告a是整數，宣告後變數可直接做運算，例如a=a+1，  
此時宣告a="test"時，文字會變成0。  
另一方面，運算時小於0的數值會預設整數變成0。  

**自訂函數**  
#!/bin/bash  
test()  
{  
echo $HOME  
pwd  
whoami  
}  
clear  
test  
或是  
function test {$HOME pwd whoami ; }  

自訂函數，內容是一串的命令，後面有加()前面就不用加上function  

**計算**
==
(( $((5%2)) == 1 ))   
[ $((5%2)) = 1 ]   
%，計算符號，用來計算餘數  
一樣的內容，記得(())要使用雙等號==  

**while read 無限閱讀**
==
while read var  
do  
echo $var  
done <txt  

把閱讀的內容一行一行放變數，再把他秀出來，  
可使用done旁邊的方法，或是在開啟檔案時加入 <txt  
閱讀的內容可以針對變數var做變化    

**while read 無限閱讀變化1**  
cat txt | while read var   
do  
echo $var  
done   

**while read 無限閱讀變化2**  
count=1    # 設定陳述式，不加空格  
cat txt01 | while read var  
do  
   echo ${var}  
   echo ${var//[!a-z]/}  
   count=$(( $count + 1 ))  
done  
echo "finish"  
exit 0  

做完更正的檔案導出到新檔案  

**陣列**
==
var=(1 2 3 4 5)  
echo ${var[0]} 等於1  
echo ${var[*]} 呼叫全部1 2 3 4 5  
echo ${#var[@]} 計算有幾個 5  

**select陣列**  
select var in ${fruits[@]}  
do  
done  



