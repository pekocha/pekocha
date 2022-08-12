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
