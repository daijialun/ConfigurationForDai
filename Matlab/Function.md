# Matlab常用函数

## 常用函数

- randperm 随机打乱一个数字序列

    y=randperm(5);
    
    ans = 2 4 1 5 3
    
- size 获取巨狠的行数和列数，A为3x4矩阵

    - size(A)
    
        ans= 3 4
        
    - s=size(A)
    
         s=3 4
         
    - [r,c]=size(A)
    
        r=3     c=4
         
    - size(X,1)，返回矩阵X的行数
    
    - size(X,2)，返回矩阵X的列数
       
- rand 产生0-1之间均匀分布的随机组成的数组

    - Y=rand(n)
    
        返回nxn随机矩阵
        
    - Y=rand(m,n)
    
        返回mxn的随机矩阵
        
- zeros 生成零矩阵

    - B=zeros(n)：生成nxn全零矩阵
    
    - B=zeros(m,n)：生成mxn全零阵       
        
- imrotate 实现旋转图像，默认逆时针旋转

    A=imrotate(A, angle, '旋转实现方法',‘Bbox’)

    - method: nearest最近邻插值法，bilinear双线性插值法，bicubic三次卷积插值法
    - Bbox( 图像的显示环境): loose宽松，crop剪切
    
- imsize 改变图像大小，B=imresize(A,m,method)或B=imresize(A,[mrows,mcols],method)

    - m：放大或缩小倍数
    - method：nearest最近邻插值法，bilinear双线性插值法，bicubic双三次插值
    
- rand()随机得到(0,1)范围内的数

- randi([1,10],10,10)得到10x10矩阵个(1,10)范围内的整数

- zscore 将数据标准化，利用标准化后的数据记性数据分析。zscore是基于原始数据的mean和std进行数据的标准化。将原始数据x使用zscore标准化到x'。Y=(X-mean(X))./std(X)

    - Y=zscore(X)
    
    样本平均值为0，方差为1；区间不确定，处理后各指标的最大值，最小值不想同；                              
    
    - [ Y, MU, SIGMA ] =zscore(X)
    
        其中，Y为X标准化后的数据，MU为mean(X)，SIGMA为std(X)
        
- assert 确保某些条件成立，否则调用系统error函数终止运行        
        
- numel 返回元素总数

    - numel(A)返回A矩阵或数组中的元素个数
    - numel(A, index1)返回A(index1)中元素的个数
    
- rem() 求整除的余数    
    
    - rem(x,y)求整除x/y的余数
    
- max() 求最大值

    - max(a)   找出矩阵每列的最大值
    - max(a, b)     如果a和b都为同维矩阵，则返回同大小矩阵，其中元素为a和b比较
    - max(a, [], dim)   dim=1时，比较a矩阵的列，同max(a)；当dim=2时，比较a矩阵的行
    - [dummy, c] = max(a, [], 2)   表示dummy存a的各行最大值，c存各行最大值位置
    
- find() 索引

    - ind = find(X)   找到矩阵X中所有非零元素，返回索引值，即位置数值；如[1 0 1 0 1]，返回[1 3 5]    
    
- reshape()    重新调整矩阵的行数，列数和维数

    - B=reshape(A,m,n)  B中元素是按列从A中得到的
    
- floor() 向下取整

    - floor(3.8)=3
    
- all() 检测矩阵中是否全为非零元素

    - B=all(A)  如果向量A中所有元素非零，则返回1，否则返回0；如果A是矩阵，返回行向量，检测每列是否全为0
    - B=all(A, dim)  dim=1，返回行向量，检测每列；dim=2，返回列向量，检测每行
    
## 用法

- .*表示矩阵对应元素相乘，而非矩阵相乘    

- X' 表示矩阵X的转置     

- 填补图像经过imrotate，imtransform，translate等变换后，结果图像周边默认使用黑色填充，可以使用以下方法：

            Img=imcomplement(Img);
            I=imrotate(Img, 60, 'nearest');
            I=imcomplement(I);
            
- 想要得到某一范围[a,b]内的随机数， 可使用:

            a+(b-a)*rand(1,1);
            
    如果想要得到只有-1和1的随机数，可用：
    
            (randi([0,1],1,1)-1/2)*2    
            
- [ ]用来构建向量(vector)或矩阵(matrix)；{ }用于cell型数组的分配和引用A(2,1)={[1 2 3; 4 5 6]}，其中A{1}=[ 1 2 3 ]，A{2}=[ 4 5 6 ]；( )用于引用数组的元素，X(3)是X的第三个元素  

- figure()是画图控制框


        