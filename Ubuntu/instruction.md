# Linux指令以及Shell用法

## 常用命令

- find path -option [-print] [-exec command] {} \;
    
    - type d 目录； f 文件；
            
        find   /tmp   -name "*.h"   -exec grep "SYSCALL_VECTOR"   {}   \; -print
        
-  sort命令是格局不同的数据类型进行排序，其语法和常用参数格式：

    sort [-bcfMnrtk] [源文件] [-o 输出文件]
    
## Shell

- 定义变量 file=/dir1/dir2/dir3/my.file.txt

    - ${file#*/}: 删除第一个/及其左边的字符串： dir1/dir2/dir3/my.file.txt
    - ${file##*/}: 删除最后一个/及其左边的字符串：my.file.txt
    - ${file#*.}: 删除第一个.及其左边的字符串：file.txt
    - ${file##*.}: 删除最后一个.及其左边的字符串：txt
    - ${file%/*}: 删除最后一个/及其右边的字符串：/dir1/dir2/dir3
    - ${file%%/*}: 删除第一个/及其右边的字符串：空
    - ${file%.*}: 删除最后一个.及其右边的字符：/dir1/dir2/dir3/my.file
    - ${file%%.*}: 删除第一个.及其右边的字符：/dir1/dir2/dir3/my
    - \#去掉左边，\%去掉右边（\#, %分别在键盘左右）；单一符号是最小匹配，两个符号是最大匹配
    
- dirname $0，返回当前路径。在命令行状态下执行，返回“.”

    在/home/admin/test/下新建test.sh，内容：
    
    1. cd `dirname $0`
    2. echo `pwd`
  
    在/home/admin/下执行sh test/test.sh，结果为/home/admin/test，即脚本目录，可知道一些和脚本一起部署的文件位置
    
- /path/to 表示设置为自己所需要的目录路径

    
    
        
