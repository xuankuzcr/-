# **第三次数字图像处理作业**
------
                                 

>姓名：郑纯然
 班级：自动化65
 学号：2160504135
 提交日期：2019年3月14日

**1.把附件图像的直方图画出；**<br/>

(1)**问题分析：**<br/>
&emsp;&emsp;强度直方图图形化显示不同的像素值在不同的强度值上的出现频率，对于灰度图像来说强度范围为[0~255]之间，对于RGB的彩色图像可以独立显示三种颜色的强度直方图。强度直方图是用来寻找灰度图像二值化阈值常用而且是有效的手段之一，若一幅灰度图像的直方图显示为两个波峰，则二值化阈值应该是这两个波峰之间的某个灰度值。同时强度直方图是调整图像对比度的重要依据。<br/>
&emsp;&emsp;直方图实现方法：对一幅灰度图像从上到下，从左到右扫描每个像素值，在每个灰度值上计算像素数目，以这些数据为基础完成图像直方图的绘制。<br/>

(2)**处理结果**<br/>

 - 各个图像的直方图<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/citywall.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/elain.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/lene.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/woman.bmp)<br/>
**自己编写的计算图像直方图的程序：**
```matlab
clc;clear;
[Im,MAP]=imread('lena.bmp');
GP=zeros(1,256);  %原图灰度概率密度函数
IM=ind2gray(Im,MAP); 
[m,n]=size(IM); 
for k=0:255               %计算原图各灰度级像素个数num 
GP(k+1)=length(find(IM==k))/(m*n);
end                       %绘制原图直方图 
figure(3);
bar(0:255,GP);
axis([0 256 0 0.02]);  
title('lena直方图');  
xlabel('灰度值');
ylabel('像素的概率分布')

```

(3)**结果分析**<br/>
&emsp;&emsp;本次实验分别采用imhist函数和自己编写的程序求取图像的直方图。经过分析发现对于某些处理后的图像得到的直方图，自己编写的在某个灰度附近有截断，是因为MATLAB中imhist会自动把map调色板进行线性扩展，导致结果的不同。将直方图与原始图像对比可以清楚的看到图像的灰度分布与图像直方图之间的关系：在暗图像中，直方图的分量集中在灰度级的低端；亮图像的直方图分量则分布于灰度级的高端。低对比度图像具有较窄的直方图，且集中于灰度级的中部；高对比度图像中直方图的分量覆盖了很宽的灰度级范围。<br/>

**2.把所有图像进行直方图均衡；输出均衡后的图像和源图像进行比对；分析改善内容；**<br/>
(1)**问题分析：**<br/>
&emsp;&emsp;直方图均衡化处理的“中心思想”是把原始图像的灰度直方图从比较集中的某个灰度区间变成在全部灰度范围内的均匀分布。直方图均衡化就是对图像进行非线性拉伸，重新分配图像像素值，使一定灰度范围内的像素数量大致相同。直方图均衡化就是把给定图像的直方图分布改变成“均匀”分布直方图分布。<br/>

(2)**处理结果**<br/>
**①citywall**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/citywall1.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/citywall2.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/citywall3.bmp)<br/>
**②elain**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/elain1.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/elain2.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/elain3.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/elain4.bmp)<br/>
**③lena**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/lena1.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/lena2.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/lena3.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/lena4.bmp)<br/>
**④woman**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/woman1.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/woman2.bmp)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/woman3.bmp)<br/>
(3)**结果分析**<br/>
经过处理得到的多组图像图像（一组四个），每组中四幅图像分别为原始图像、直方图均衡化后的图像、原始图像的直方图以及均衡化后图像的直方图。从直方图上可以观察到灰度分布确实更加均匀并且占据整个灰度级范围；从图像上可以观察到，图像对比的变大，灰度色调变化范围加大。同时，也注意到有些图像的均衡效果不是很好，所以可以发现直方图均衡并不是适用于所有的图像。一般意义上说，可以得出这样的结论：若一幅图像的像素倾向于占据整个可能的灰度级并且分布均匀，则该图像会有高对比度的外观并展示灰色调的较大变化。最终效果将得到一幅灰度细节较为丰富且动态变化范围较大的图像。<br/>


**3.进一步把图像按照对源图像直方图的观察，各自自行指定不同源图像的直方图，进行直方图匹配，进行图像增强；**<br/>
**4.对elain和lena图像进行7*7的局部直方图增强；**<br/>

(1)**问题分析：**<br/>
&emsp;&emsp;直方图匹配（histogram matching）：将图像直方图以标准图像的直方图为标准作变换,使两图像的直方图相同和近似,从而使两幅图像具有类似的色调和反差。<br/><br/>
&emsp;&emsp;直方图匹配的原理：对两个直方图都做均衡化，变成相同的归一化的均匀直方图，以此均匀直方图为媒介，再对参考图像做均衡化的逆运算。<br/>
(2)**处理结果**<br/>
**①citywall**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/1.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/2.png)<br/>
**②elain**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/3.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/4.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/5.png)<br/>
**③lena**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/6.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/7.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/8.png)<br/>
**④woman**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/9.png)<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/10.png)<br/>
(3)**结果分析**<br/>
对比原始图像的直方图、匹配图的直方图以及增强后图像的直方图可知，基本完成了直方图匹配。但也注意到：原始图像直方图和匹配后图像的直方图并没有完全一致。是因为原始图像中多个灰度值映射到增强后图像的同一个灰度值。对比原始图像以及增强后的图像可知，经过直方图匹配后，大部分图像的效果得到了一定的改善。但有些图像的效果并没有改善甚至变差了，可能是因为要求匹配的直方图选择不合适导致的或者是要求进行直方图匹配的图像的直方图灰度值分布过于集中所导致。<br/>

**5.利用直方图对图像elain和woman进行分割**<br/>
(1)**问题分析：**<br/>
&emsp;&emsp; 利用直方图进行阈值分割方法的原理：如果图像所包括的背景区域与所分的目标区域在灰度上有着明显的区别，那这样的图像的灰度直方图就会呈现很明显的双峰状。其中一个峰值对应的是背景区域的灰度，而另一个峰值对应的是前景区域。理想中的图像的灰度直方图，其背景灰度和目标灰度应对应两个不同的灰度峰值，应选取位于两峰之间的谷值作为阈值，就很快地将一副图像的背景与目标分割开了。<br/>
&emsp;&emsp;可以先对图像进行锐化或者平滑的预处理，改善图像质量。<br/>
(2)**处理结果**<br/>
**①利用graythresh函数直接寻找阈值level**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/final_matlab.bmp)<br/>
**①根据直方图手动修改**<br/>
![zcr](https://github.com/xuankuzcr/hw3/blob/master/final3.bmp)<br/>
(3)**结果分析**<br/>
&emsp;&emsp;由实验输出结果可知直接调用graythresh达到了对图像进行分割的目的，但自己编写程序手动修改阈值时不能够较好地将前景和背景分开，通过观察直方图可知，虽然经典的直方图算法实现简单，但只是针对少数不同类别的物体且彼此灰度相差很大时，才能进行有效的分割。当原始图像的双峰不明显时，分割得不到理想的图像。<br/>

> 附录
【参考文献】
[1] 冈萨雷斯.数字图像处理（第三版）北京：电子工业出版社，2011.<br/>
[2] 周品.MATLAB数字图像处理 北京：清华大学出版社，2012.<br/>
[3] 杨杰.数字图像处理及MATLAB实现 北京：电子工业出版社，2010.<br/>


