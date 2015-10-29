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