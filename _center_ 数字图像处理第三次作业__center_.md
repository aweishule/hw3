#<center> 数字图像处理第三次作业</center>

------

<center>自动化少61</center>

<center>魏俊哲</center>

<center>2140506024</center>

<center>2019.3.19</center>

　摘要：本次报告主要记录数字图像处理第三次作业中的各项任务完成情况。本次作业以如matlab2016a为平台，结合matlab函数编程实现对所给图像文件的相关处理：1.把附件图像的直方图画出；2,把所有图像进行直方图均衡；输出均衡后的图像和源图像进行比对；分析改善内容；3,进一步把图像按照对源图像直方图的观察，各自指定不同源图像的直方图，进行直方图匹配，进行图像増强。4.对elain和lena图像进行7*7的局部直方图增强；5.利用直方图对图像elain和woman进行分割；以上任务完成后均得到了预期的结果。




> 1.把附件图像的直方图画出 实验原理及方法

### 原理说明

图像直方图显示不同的像素值在不同的强度值上的出现频率，它是一个二维图，横坐标表示图像中各个像素点的灰度级，纵坐标为各个灰度级上图像各个像素点出现的次数或概率。 它可以用来寻找灰度图像二值化阈值和调整图像对比度，如果一幅灰度图像的直方图显示为两个波峰，则二值化阈值应该是这两个波峰之间的某个灰度值。绘制直方图的原理是利用matlab的imread函数读取图像数据点，对数据点的值进行排序，统计每个灰度值出现的次数，利用这些数据值即可绘出直方图。在matlab中可直接利用imhist函数完成以上过程。
另外需要注意的一点是，所给的8幅经变亮或变暗处理的图像是索引图，调色板查看表头信息可以发现调色板中规定了一百多种灰度信息，然而图像中存在大量未定义的像素，photoshop和matlab中默认为255灰度白色，使用系统自带的图片查看时则显示为0灰度黑色，容易引起混淆。在matlab中可以使用imread读出调色板信息存到map中，可以使用ind2gray函数将他们转换为灰度图像后进行操作。

------

### 处理结果如下：


![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/canny4.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/womanimh.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/elainimh.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/lenaimhist.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/ctwim.jpg)


###结果分析
 直方图反映了图像的概率统计特征，虽然不够直观但可以看出图像的概貌，例如较暗的图像直方图低灰度级处聚集，较亮的图像直方图高灰度级处聚集。
[1]:https://raw.githubusercontent.com/aweishule/dipnew/master/ctwim.jpg
dipnew/ctwim.jpg 
> 2.把所有图像进行直方图均衡；输出均衡后的图像和源图像进行比对；分析改善内容；
###  原理说明

直方图均衡化是图像处理领域中利用图像直方图对对比度进行调整的方法。该方法通过 灰度变换将一幅图像转换为另一幅具有均衡直方图，即在每个灰度级上都具有相同的象素点数的图像。数学上可以证明连续情况下的均衡性，在数字图像处理实际应用中使用离散情况，也能起到较大的作用。直方图均衡处理是以累计分布函数为基础的直方图修改法。在matlab平台上先用imread函数读取图像的图像数据，然后利用histeq函数进行直方图均衡操作，最后用imhist和imshow函数分别绘制经直方图均衡化的直方图和bmp图像

### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/ctw2%201.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/ctw2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/ctw2%202.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/elain2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/elain2%201.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/elain2%202.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/lena2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/lena2%201.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/lena2%202.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/woman2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/woman2%202.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/woman2%201.jpg)
### 结果分析
几组情况相近，以woman组为例。分别与处理前的原图像相比，发现woman，woman2变亮，对比度有一定程度的增强，但同时也存在一些细节的消失，某些地方经处理后对比度不自然的过分增强。womanl原来亮的地方经处理后变暗，原来暗的地方变亮，对比度减弱但是更符合人体视觉习惯，细节更丰富。 
> 3.进一步把图像按照对源图像直方图的观察，各自自行指定不同源图像的直方图，进行直方图匹配，进行图像增强；

### 原理说明
直方图匹配：是指使一幅图像的直方图变成规定形状的直方图而进行的图像增强方法，其目的是通过选择不同的匹配对象对一定灰度级范围内的图像进行有目的的增强，以突出其重点，达到要求的效果。由于其他图像是经原图像进行变亮变暗处理后得到,而且观察发现原图像效果最好，所以本题中将图像直方图以原图像的直方图为标准作变换,使两图像的直方图相同和近似，从而使两幅图像具有类似的色调和反差，达到增强图像，突出细节的目的。可利用matlab的imhist函数分别得到原图像与需匹配图像的直方图，然后利用histeq函数进行直方图匹配后分别画出经直方图匹配的图像及其直方图。


### 处理结果

![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/m%20lena1.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/m%20lena2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/match%20woman1.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/m%20woman2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/mctw1.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/mctw2.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/melain1.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/melain2.jpg)
### 结果分析
匹配后的图像的直方图分布在整个空间当中，与原图像的直方图形状更为相似。匹配后的图像对比度变大，图像可识别性增强，同时细节处还能比较清晰，但也存在某些细节消失，和部分部位对比度过度增强导致些许不自然，但整体效果较好。由此可知，直方图匹配能够用已知的模板或者是预想达到的直方图去匹配处理的图像，使处理后的图像的概率密度曲线最接近模板的概率密度曲线。从而达到直方图匹配的目的，而最关键的问题是如何选定这个模板，才能达到图像处理效果，一般可根据被处理图像的直方图和图像本身的特征，经过函数转换得到我们需要的直方图，或者是找一个现成的直方图模板。第一个方法比较有针对性，但是技术要求比较高。第二个方法相对容易，这里采用的就是第二方法。

> 4.对elain和lena图像进行7*7的局部直方图增强；

### 原理说明
对原图像非边缘的每一个点取7x7的邻域进行直方图均衡，然后取中心点，由于算法复杂度过大，所以只处理了一张图像。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/locallena.jpg)
### 结果分析

从图中可以看出，处理好的图像直方图十分规律。


> 5.利用直方图对图像elain和woman进行分割；

### 原理说明
直方图分割的阈值方法的原理是，如果图像所包括的背景区域与所分的目标区域大小可比，而且两者在灰度上有着明显的去表，那么这样的图像的灰度上有着明显的去表，那么这样的图像的灰度直方图就会呈现很明显的双峰状；其中一个峰值对应的应该是背景区域的灰度；而另一个峰值对应的就是目标灰度了；理想中的图像的灰度直方图，其背景灰度和目标灰度应对应两个不同过的灰度峰值，所以选取位于两峰之间的谷值作为阈值，就很快地将一副图像的背景与目标分割开了。经典的直方图算法实现简单，但是这只是针对少数不同类别的物体彼此灰度相差很大时，才能进行有效的分割。当原始图像的双峰不明显时，分割得不到理想的图像。先对图像进行锐化或者平滑处理，使之达到改善图像的质量的实际应用的要求，这个方法是当图像的边缘细节与图像商上梯度的整体强度有关，图像边缘越强，图像的细节效果越明显。
使用matlab提供的函数：graythresh使用最大类间方差法找到图片的一个合适的阈值（threshold）。在使用im2bw函数将灰度图像转换为二值图像时，需要设定一个阈值，这个函数可以帮助我们获得一个合适的阈值。利用这个阈值通常比人为设定的阈值能更好地把一张灰度图像转换为二值图像。 im2bw(I, level)使用阈值（threshold）变换法把灰度图像（grayscale image）转换成二值图像，其中level就是设置阈值的。level取值范围[0, 1]。
### 处理结果
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/seg%20elain.jpg)
![Aaron Swartz](https://raw.githubusercontent.com/aweishule/dipnew/master/segwoman.jpg)
### 结果分析
基本实现了分割的目的，值得注意的是由于把两幅图像的直方图当做双峰处理是不够精确的，所以使用多阈值分割可以达到更好效果。

### 附录
参考文献：Rafael C. Gonzalez., et al. 数字图像处理（第三版）, 电子工业出版社，2011.

