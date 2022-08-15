**go語言**
==
C語言的速度，java的物件導向能力，python語言的簡潔，  
套件比開發語言有名，使用go語言開發的有docker(Container技術)跟Kubernetes    

**開發 Golang 網站**
==
1.cd; mkdir mygo; cd mygo  
建立使用的資料夾   
2.echo 'package main  
import (  
	"fmt"  
	"log"  
	"net/http"  
)  
func handler(w http.ResponseWriter, r *http.Request) {  
	fmt.Fprintln(w, "Hello, 世界")  
}
func main() {  
	http.HandleFunc("/", handler)  
	log.Fatal(http.ListenAndServe(":8888", nil))  
}' > main.go  
重導輸出  
3.CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a main.go  
編譯成電腦看得懂的機械碼(機器內老師有裝go語言套件，所以可以用)  
4.執行導出的main檔，會一直卡住，但不用理他  
5.輸入IP加上:8888進入網站  
6.結束執行按ctrl+c  
