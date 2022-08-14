**快篩試劑調查**
==
#!/bin/bash  
for c in 金門 馬祖 連江   
do  
  echo "$c 今日提供快篩試劑店家:"  
  echo "________________________"  
  cat fsdata.csv | cut -d',' -f2,3,8 | grep "$c"  
  echo "$c OK!"  
done  

n=$(cat fsdata.csv | grep "$c" |wc -l)  
echo "$c 共有 $n 家醫療機構有提供快篩試劑"  
echo ____________________________________  


**不知道是什麼**
==  
#!/bin/bash  
[ "$USER" != "root" ] && echo "需要SUDO權限" && exit  
read -p "請輸入要加入幾個port" ans1  
brctl addbr macsw8  
echo "建立macsw8"  
ifconfig macsw8 172.16.20.254 netmask 255.255.255.0 up  
echo '設定ifconfig macsw8 172.16.20.254 netmask 255.255.255.0 up'  
for ((n=0;n<=ans1;n=n+1))  
do  
sudo tunctl -b -u ${USER}  
done  

for((m=0;m<=$ans1;m=m+1))  
do  
sudo ifconfig tap${m} up  
sudo brctl addif macsw8 tap${m}  
done  

brctl show  
