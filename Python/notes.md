# Python笔记

- 默认参数：必选参数在前，默认参数在后；变化大的参数放前，变化小的参数放后；一定要用不可便对象（如果是可变对象，运行会有逻辑错误）

            def power(x,n=2)      

- 可变参数：传入的参数个数是可变的，可以是1个，2个或任意个。在函数中，定义可变参数和定义list或tuple相比，仅仅在参数前加上*号。

            def calc(*number);
    
    调用时，普通调用方式需先组装一个list或tuple，例如calc([1,2,3])；而利用可变参数，调用函数的方式可为calc(1,2,3);如果已经有list或tuple，nums=[1,2,3]，要调用一个可变参数，calc(*nums)
    
- 关键字参数：允许传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict，即kw为dict类型

            def person(name, age, **kw);

- 参数组合，参数定义的顺序为：必选参数，默认参数，可变参数，关键字参数
          
- **\*args和\*\*kw是Python习惯用法**          

- 切片：L[1:3]作用与[L[0],L[1],L[2]]相同；L[:10:2]，省略0，取间隔为2；L[::5]，所有数，间隔为5

- range(1,5)从1到5，不包含5，返回[1,2,3,4]；range(1,5,2)从1到5，间隔为2，返回[1,3]

- 列表生成式：用来生成list的简便写法，[x*x for x in range(1,5)]，返回[1,4,9,16]

- isinstance()判断变量类型

- **生成器**：创建generator，将列表生成式[]改为()，之后使用for循环迭代
    
            g=generator(x*x for x in range(10))
            
- yield关键字是函数变为generator，在调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次`yield`语句位置继续执行 

- 函数式编程：允许把函数本身作为参数传入另一个函数，还允许返回一个函数

- 高阶函数：一个函数可以接受另一个函数作为参数，即让函数的参数能够接受别的函数。函数式编程就是指这种高度抽象的编程范式

- map()函数接受两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回

            map(f, [1,2,3,4,5])
            
    返回[1,4,9,16,25]
    
- reduce()函数接受两个参数，一个是函数，一个是序列，reduce把结果继续和序列的下一个元素做累计计算

            reduce(f,[x1,x2,x3,x4])=f(f(f(x1, x2), x3) ,4)
            
- filter()函数用于过滤序列，把传入的函数依次作用于每个元素，然后根据返回值决定保留还是丢弃该元素

- 模块：一个py文件就是一个模块（module），引入目录组织模块方法，即包（packge）避免模块名的冲突。abc.py与xyz.py分别为abc与xyz模块，二者的包为mycompany，则模块名为`mycompany.abc`                    
                 与`mycompany.xyz`。每个包目录下都有`_int_.py`文件，声明为包，其本身就是一个模块，模块名为`mycompany`
                 
- 文件开头使用`#!usr/bin/env python` 可使文件在以脚本形式运行

- 任何模块代码的第一个字符串都被视为模块的文档注释

- 作用域：

    - 正常函数和变量名：abc，x123
    -  特殊变量或函数_xxx_，可被直接引用，但是有特殊用途，\_author\_，\_name\_
    - 非公开函数或变量_xxx，不应该被直接引用，_abc
    
    通过这种方法，将外部不需要引用的函数全部定义成private，只有外部需要引用的函数才定义为public      
    
- 实例的变量名以_开头，变成了私有变量，只有内部可以访问，外部不能访问，如_score, _name

- 变量名类似_xxx_为特殊变量，特殊变量是可以直接访问的，不是private变量

- 定义好了`Student`类，可根据`Student`类创建实例，创建实例是通过类名+()实现的

          bart=Student();
          
- 多态：只需要知道其是父类，无需确切知道其子类型，即可调用其成员函数，具体函数有该对象的确切类型决定

- 在地啊用类实例方法时，尽量把变量视作父类类型，这样，所有子类类型都可以正常被接收

- 任何时候，如果没有合适的类可以继承，就继承自object类

- type()判断对象类型，python将每种type类型都定义好了常量，放在`types`模块中，使用之前，导入即可。有一种类型`TypeType`，所有类型本身的类型就是`TyepType`

            type([])==types.ListType
            type('abc')==types.StringType        
            
- isinstance()函数判断（对于class的继承关系来说，使用type()不方便）

            a=Animal()
            isinstance(a, Animal)
            
- dir()获得一个对象的所有属性和方法，返回一个包含字符串的list

- len(), lower(), getattr(), setattr(), hasattr()函数

- 错误处理

    - try, exception, finally
    - 记录错误： logging模块
    - 调用堆栈：错误如果没有被捕获，则一直往上抛
    - 抛出错误：raise语句跑出错误案例            
    
- assert断言，其后的表达式应该是True，否则，后面的代码会除错；如果断言失败，assert就会抛出`AssertionError`

- 文件读写是通过`open()`函数打开的文件对象完成的，使用`with`语句操作文件IO是个好习惯

            try:
                f=open('/path/to/file','r')
                print f.read()
            finally:    
                if f:
                    f.close()
                    
    with...as语句与try...finally语句相同，且不必使用f.close()方法
    
            with open('/path/to/file','r') as f:
                print f.read()
                
- read(size)每次最多读取size个字节的内容；readline()每次读取一行内容；readlines()一次读取所有内容并按行返回list

- 写文件时，操作系统往往不会立刻吧数据写进磁盘，而是放到内存缓存起来，空闲时候再慢慢写入。只有调用close()时，操作系统才保证把没有写入的数据全部写入磁盘，没有调用`close()`的后果是数据可能只写了一部分到磁盘，剩下的都丢失了。所以用`with`语句来得保险

- 错坐文件和目录的函数一部分在`os`模块中，一部分放在`os.path`模块中

            os.path.abspath('.')
            os.path.join('oldpath','dirname')
            os.mkdir('path')
            os.rmdir('path')   
            
- 把两个路径合成一个时，不要直接拼字符串，通过`os.path.join()`函数，可以正确处理不同操作系统的路径分隔符

- 拆分路径时，也不要直接取拆字符串，通过`os.path.split()`；而os.path.splitext()可得到文件的拓展名

            >>> os.path.split('/users/michael/file.txt')
            ('/users/michael','file.txt')
            >>> os.path.splitext('/users/michael/file.txt')
            ('/users/michael/file','.txt')
            
- 文件重命名`os.rename()`；删除文件`os.remove()`            

- 复制文件函数`copyfile()`函数在`shutil`模块中
                                              