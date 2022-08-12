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
