# hello-world
just a repository
I=imread('photo1.jpg');              %图像输入
I1=rgb2gray(I);                 %转换成灰度图像I1        
I2=wiener2(I1,[5,5]);            %对图像进行维纳滤波I2  
I3=edge(I2,'sobel', 'horizontal');%用Sobel水平算子对图像边缘化
I3=imcrop(I3,[0 0 500 100]);%对图像进行剪切，保留图像中的一条直线，减小运算量
theta=0:179;    %设置选择角度
r=radon(I3,theta);%对图像进行Radon变换
[m,n]=size(r);
c=1;
for i=1:m
    for j=1:n
        if  r(1,1)<r(i,j)
           r(1,1)=r(i,j);
            c=j;
        end
    end
end                              %检测Radon变换矩阵中的峰值所对应的列坐标
rot=90-c;%确定旋转角度
I4=imrotate(I2,rot,'crop');        %对图像进行旋转矫正
set(0,'defaultFigurePosition',[100,100,1200,450]); %修改图形图像位置的默认设置
set(0,'defaultFigureColor',[1 1 1])                 %修改图形背景颜色的设置
figure,                                             %显示处理结果
subplot(121),imshow(I),title('原始车牌图像灰度图像')
subplot(122),imshow(I2),title('预处理后车牌灰度图像')
figure,
subplot(121),imshow(I3),title('边缘检测后车牌图像')
subplot(122),imshow(I4),title('校正后车牌图像')
