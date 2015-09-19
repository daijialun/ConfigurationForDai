# C++ Primer Plus 读书笔记

## Chapter 10 类和对象

- 抽象：将问题的本质特征抽象出来，根据特征来描述解决方案

- 指定基本类型：
    - 决定数据对象需要的内存数量
    - 决定如何解释内存中的位数
    - 决定可使用数据对象执行的操作或方法
    
 - ** 类**是一种将抽象转换为用户类型的C++工具。
 
     类定义：
     - 类声明：数据成员描述数据部分，成员函数描述公有接口
     - 类方法：如何实现类成员函数
     
 - 通常，接口（类定义）放在头文件中，将实现（类方法代码）放在源代码中
 
 - **类名首字母大写**
 
 - 对象/实例：声明类类型的具体变量
 
 - **公有成员函数**是程序和对象的私有成员之间的桥梁，提供了对象和程序之间的接口
 
 - 类的默认访问类型为private
 
 - 定义成员函数时，用作用域解析运算符（::）来标识函数所属类；类方法可以访问类private组件
 
 - 内敛函数的特殊规则：每个使用的文件中都要对其进行定义，保证内联定义对多文件程序中的其他文件都可用。**可通过将内联定义放在定义类的头文件中**
 
 - 创建的新对象都有独立的存储空间，存储其内部变量和类成员；但是同一个类下的所有对象只共享同一组类方法
 
        Stock kate；
        Stock joe;
        
    kate.shares占一个内存块，joe.shares占据另一个内存块。kate.show()和joe.show()都调用同一个方法（函数）
    
### 构造函数和析构函数

#### 构造函数

- 构造函数没有声明类型，即没有返回类型

- 构造函数的参数表示的不是类成员，而是赋给类成员的值。因此，参数名不能与类成员相同

        Stock::Stock( const string &company, long shares, double share_val)
        { ... }
        
      改为：
        
        Stock::Stock( const string &company, long sm double d)
        
- **为了避免以上混乱，一种是在数据成员名中使用m_前缀，m_company；另一种是成员名售后后缀_，company_

- 初始化对象：
      - 显示 
      
            Stock food=Stock("N" ,250,1.5)
            
      - 隐式
      
            Stock garment("M", 50, 2.5)
            
- 为类定义了构造函数后，就必须为其提供默认构造函数。**定义默认构造函数方式：**
    - 给已有构造函数的所有参数提供默认值：
    
        Stock( const string &co="Error", int n=0, double pr=0.0);
        
   - **（常用）**函数重载，一个没有参数的构造函数：
   
        Stock::Stock()
        {
                company="no";
                shares=0;
                share_val=0.0;
        }
        
- **默认构造函数**可以没有任何参数；如果有，必须给所有参数都提供默认值

#### 析构函数

析构函数的类名前加~，即~Stock()，析构函数没有参数

- 默认情况下，将一个对象赋给同类型的另一个对象时， C++将源对象的每个数据成员的内容赋值到目标对象中相应的数据成员中

- 将新值赋给对象，stock1=Stock( "Nifty", 10, 50)，让构造函数创建新的、临时对象，将其内容复制过去，随后调用析构，删除临时对象

- Stock stock2=Stock("Boffo", 2,10);

    Stock1=Stock("Nity",10.50); 
    
    第一条语句是初始化**（常用）**，创建有指定值对象；第二条是赋值，在赋值前创建临时对象
    
- const成员函数 void stock::show() const 保证类方法不修改调用对象

### this指针

如果一个类成员函数涉及两个对象，即调用它的对象以及其他对象，需要使用this指针

- Stock为类，则

    const Stock &topval(const Stock & s) const
    
    const Stock &s表示不修改显式表示的对象，最后const表示函数不修改隐式访问对象，前面的const表示返回类型不变
    
    调用为top=stock1.topval(stock2)
    
- this指针指向调用对象，引用整个调用对象，则使用表达式*this；函数括号后面使用const，则不能使用this修改对象的值

#### 对象数组

- 声明对象数组与声明标准类型数组相同：Stock mystuff[4];

- 类包含多个构造函数，对不同元素使用不同的构造函数

    Stock stocks[3]={ Stock("NanoSm",20), Stock(), Stock("Mono") };
    
- 创建类对象数组，这个类必须要有默认构造数组。在初始化时，首先使用默认构造函数创建数组


### 类作用域

- 类中定义的名称（数据成员和成员函数）作用域为整个类

#### 定义常量，作用域为整个类
    
private: const int M=12; 不行，声明只描述了对象形式，没有创建对象

- **类中声明一个枚举**，用枚举为整型常量提供作用域为整个类的符号名称，其不创建类数据成员，只是一个符号名称

    private: enum { M=12 };
    
- **关键字static**，该常量将与其他静态变量存储在一起，不存储在对象中。即一个M常量，被所有对象分享

### 抽象数据类型

抽象数据类型（abstract data type, ADT）以通用的方式描述数据类型，没有引入语言或实现细节


## Chapter11 使用类

### 运算符重载

函数重载是用同名函数完成相同的基本操作，甚至这种操作被用于不同的数据类型    

- 运算符函数格式： operator op(argument-list)，如operator+()。不能虚构新的运算符

- district=sid+sara  编译器发现是操作数sara，是类对象，使用相应运算符函数替换上述运算符 district=sid.operator+(sara) ;  隐式使用sid，显式使用sara对象

- **不要返回指向局部变量或者临时对象的引用。**函数执行后，局部变量和临时对象将消失，引用将指向不存的数据。例如：

    Time & Time::Sum(const Time &T) const
    {Time sum; sum=T;return sum;}由于函数引用sum对象，sum对象为局部变量，函数结束删除，则最终指向不存在对象
    
    Time & Time::Sum(const Time &T) const
    {Time sum; sum=T;return sum;} 由于函数有返回对象，将创建对象副本，调用函数可以使用
    
 - 重载限制：
    - 重载后的运算符必须至少有一个操作数是用户定义的类型，防止用户为标准类型重载运算符
    - 使用运算符时不能违反运算符原来的句法规则。例如，不能将求模运算符(%)重载成+
    - 不能创建新运算符
    - 不能重载以下运算符：sizeof, .*, ::, ?:等
    - 下列运算符智能通过成员函数进行重载：=:, ():, []:, ->
    
### 友元

友元： 友元函数，友元类，友元成员函数；关键字**friend**

**友元函数：**

- 将友元函数的原型放在类声明中，在声明前加上friend：friend Time operator*(double m, const Time & t);
        
- operator *() 在**类声明中声明的，但不是成员函数，不能使用成员运算符来调用，但是与成员函数的访问权限相同**

#### 常用友元：重载<<运算符

- <<的第一种重载版本：

    - cout << trip;  使用友元函数，重载运算符
    
        void operator<< (ostream & os, const Time & t) { os << t.h << t.m; }
        
     - operator<<()函数是Time类的友元函数，该函数不是ostream类的友元

- <<的第二种重载版本

    trip为对象，实现cout << "Time" <<trip；
    
    ostream & operator<<(ostream & os, const Time & t){os <<t.hours <<t.min; return os}
    
- **只有在类声明中的原型才能使用friend关键字。除非函数定义也是原型，否则不能在函数定义中使用该关键字

- 重载运算符，用于成员函数或非成员函数（稍好）

### 重载：矢量类
    
-在Vector类中声明friend std::ostream & operator<<(std::ostream & os, const Vector & v);  

    由于operator<<()是友元函数，而不在类作用域中，因此必须使用Vector::Rect，而不能使用RECT。由于这个友元函数在名称空间VECTOR中，无需使用全限定名VECTOR::Vector::RECT。
    
- 对已重载的运算符进行重载：使用的运算符数量与相应的内置C++运算符相同，就可多次重载同一个运算符

### 类的自动转换和强制类型转换

#### 类的自动转换

- 任何接受唯一一个参数的构造函数都可被用作转换函数，将与该参数相同类型的值转为类；即将与该参数相同类型的值赋给对象，则自动调用构造函数
    
#### 转换函数

- 要将类对象转换为其他类型，必须定义转换函数，支出如何进行这种转换；转换函数必须是成员函数

- 强制类型转换：将类类型转换为某种类型 operator *typeName()*;

    - 转换函数必须是成员函数
    - 转换函数不能指定返回类型
    - 转换函数不能有参数
    - 必须返回转换后的值
    
    Vector转换为double类型的函数: Vector::operator double(){ return a_doule_value; }   
    但是最好不要依赖于这种隐式转换函数
    
- 用功能相同的非转换函数替换该转换函数，但仅在被显式地调用，该函数才会被执行
    Time::operator int(){ return int (hour+1);}替换为 int Time::Time_to_Int(){ return int (hour+1);}
       
      则int plb=poppins为非法表示；int plb=popp.Time_to_Int();
      
## Chapter 12 类的动态内存分配

### 动态内存和类

- 类声明中，只能声明静态成员变量，但是不能初始化。**静态数据成员在类声明hpp中声明，在类方法cpp文件中初始化，不需要使用关键字static**

    声明：static int num_strings;
    初始化：int StringBad::num_strings=0;
    
    初始化在在类声明hpp文件中进行。因为可能有多个文件包含头文件，如果在hpp中初始化，会出现多次初始化，引发错误
    
    **静态成员是整型或枚举型const，则可以在类声明中初始化**
    
- 构造函数中使用new分配内存时，必须在相应析构函数中使用delete来释放内存。如果使用new[]来分配内存，则应使用delete[]释放内存
    
- 特殊成员函数：
    - 默认构造函数（如果没有定义构造函数）
    - 默认西沟函数（如没定义）
    - 复制构造函数（如没定义）
    - 赋值运算符（如没定义）
    - 地址运算符（如没定义）
    
- 如果没提供任何构造函数，C++将自动创建默认构造函数（不接受任何参数，也不执行任何操作），为了解决 Klunk lunk; 这类问题； 
   
    **默认构造函数：**
     
     - 没有参数
     - 所有参数都有默认值
    
    **复制构造函数：**
    
     - 用于初始化，而不是常规赋值
     - 表现为指向对象的引用左右参数，例如StringBad( const String & )
     - 将新对象显式地初始化现有对象，常使用赋值构造函数，例如：
        - String ditto(motto);
        - String metoo=motto;
        - String also=String(motto);
        - String *pStringBad=new String(motto);
     - **按值传递和返回对象，都将调用复制构造函数**
     - 默认赋值函数，只是直接复制成员变量值，即只复制指针地址，并不复制指针内容；通过显式复制构造函数，StringBad::StringBad(const StringBad &st) {str=new char[len+1]; strcpy(str, st.str);}则复制指针内容，如果之前对象删除，也不会影响
   
### 改进的String类

- C++11，nullptr空指针，即str=nullptr  

- 中括号运算符[]，可通过operator[]()来重载该运算符，一个操作数位于[之前，另一个操作数位于[]之间。例如，city[0]中，city是第一个操作数，[]是运算符，0是第二个操作数

- String::show() const表示成员函数show()不改变成员变量；const String answer("fut")表示常量对象

- **静态类成员函数**，可用类名和作用域解析运算符来调用。例如， static int HowMany(){return num;}，则调用方式为int count=String::HowMany();

    使用静态类成员函数，注意：
    
    - 不能通过对象调用静态成员函数，不能使用this指针（其为公共部分）
    - 只能使用静态数据成员，如num_thing，不能使用str与len
    
### 构造函数使用new注意

- 构造函数使用new初始化指针成员，则在析构中使用delete

- new []对应于delete []

- 如果有多个构造函数，必须以相同的方式使用new，都带中括号，或者都不带。因为只有一个析构函数，所有构造函数必须与其兼容

- 应定义一个复制构造函数，通过深度复制将一个对象初始化为另一个对象。String::String( const String &st) { str=new char[len+1];strcpy(str, st.str);}。即复制构造函数应复制数据，而不仅仅是数据地址。

- 应定义一个复制运算符，深度复制一个对象给另一个对象。功能：检查自我赋值，释放成员以前指针，复制数据非地址，并返回指向调用对象的引用。

### 返回对象

- 如果函数要返回局部对象，应返回对象，不能是指向对象的引用。这种情况，将使用复制构造函数来生成返回的对象。

- 函数返回一个没有公有复制构造函数的类（如ostream类）的对象，必须返回一个指向这种对象的引用。

- 有些函数（如重载运算符）可以返回对象，也可以返回指向对象的引用。这种情况，**首先使用引用**，效率更高。

### 指向对象的指针

使用new初始化对象：

- Class_name *pclass=new Class_name(value)，其中Class_name是类，value类型为Type_name；随后使用构造函数Class_name(Type_name);

- 默认构造函数，则Class_name *ptr=new
 Class_name；
 
- 例如， String *favorite=new String(test);

- Act *pt=new Act; delete pr; 对pt使用delete运算符时，将调用动态对象pt的析构函数

- delete只释放对象占用空间，对于成员变量所指向的内存，使用析构函数完成

- 如果对象是动态变量（普通成员变量，非静态），new，则当执行玩定义该对象的程序块时，将调用该对象的析构函数

- **对象是用new创建的，则必须显式使用delete删除对象时，析构函数才会被调用。**

- 指针和对象：
    
      - 常规表示对象指针 String *glamour
      - 对象初始化指针 String *first=& saying[0];
      - 使用new初始化指针，创建新对象 String *favorite=new String(saying[choice])
      - 调用构造函数，初始化新对象 String *gleep=new String；String *glop=new String("my")

