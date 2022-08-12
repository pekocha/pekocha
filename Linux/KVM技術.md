**KVM**
==
**Linus Torvalds** linux開發人(Linux 脫襪子)  

所以只要是Linux作業系統，一定可以使用KVM這個技術。  

KVM是用來幫我們跑虛擬技術的東西，只要是虛擬技術，都是模擬出來的，  
但是INTEL VT以及 AMD SVM，這兩家使用KVM的話，那虛擬機器使用的就是真實的CPU和記憶體，  
硬體輔助虛擬化(網路、硬碟使用模擬的)。  

QEMU 通通是模擬技術，不是真實的  
KVM CPU和記憶體是真實的，網路卡硬碟是虛擬的  

硬體輔助虛擬化  
Intel 的是VT-x  
AMD的是SVM  

**Hypervisor**
==
裸機架構（Bare-Metal）  
作業系統本身就包含虛擬化技術  
寄居架構（Hosted）  
作業系統本身不包含虛擬化技術  
需要額外下載、安裝  
