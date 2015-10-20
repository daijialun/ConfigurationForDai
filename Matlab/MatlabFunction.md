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
        
## 用法

- .*表示矩阵对应元素相乘，而非矩阵相乘    

- X' 表示矩阵X的转置     