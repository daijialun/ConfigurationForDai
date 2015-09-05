# Linux下常用指令

- find path -option [-print] [-exec command] {} \;
    
    - type d 目录； f 文件；
            
        find   /tmp   -name "*.h"   -exec grep "SYSCALL_VECTOR"   {}   \; -print
        
