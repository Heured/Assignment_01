# Assignment_01
直方图、高斯滤波、直方图均衡  
  
  
ps：所需模块有pillow、scipy、pcv、matplotlib
  
  
原图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/image_forTest.jpg)
## 直方图
  
图像轮廓线和图线等高线。在画图像轮廓前需要转换为灰度图像，因为轮廓需要获取每个坐标[x,y]位置的像素值。  
  
  例：  
```python
 # -*- coding: utf-8 -*-
from PIL import Image
from pylab import *

# 添加中文字体支持
from matplotlib.font_manager import FontProperties
font = FontProperties(fname=r"c:\windows\fonts\SimSun.ttc", size=14)
im = array(Image.open('./data/image_forTest.jpg').convert('L'))  # 打开图像，并转成灰度图像

figure()
subplot(121)
gray()
contour(im, origin='image')
axis('equal')
axis('off')
title(u'图像轮廓', fontproperties=font)

subplot(122)
hist(im.flatten(), 128)
title(u'图像直方图', fontproperties=font)
plt.xlim([0,260])
plt.ylim([0,11000])

show()
```
  
路径: [直方图](https://github.com/Heured/Assignment_01/blob/master/codes/zhiFangtu.py)  

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/Zft.JPG)
  
## 直方图均衡
  
一个极其有用的例子是灰度变换后进行直方图均衡化。图像均衡化作为预处理操作，在归一化图像强度时是一个很好的方式，并且通过直方图均衡化可以增加图像对比度。  


  例：  
```python
 # -*- coding: utf-8 -*-
from PIL import Image
from pylab import *
from PCV.tools import imtools

# 添加中文字体支持
from matplotlib.font_manager import FontProperties
font = FontProperties(fname=r"c:\windows\fonts\SimSun.ttc", size=14)

im = array(Image.open('./data/image_forTest.jpg').convert('L'))  # 打开图像，并转成灰度图像
# im = array(Image.open('../data/AquaTermi_lowcontrast.JPG').convert('L'))
im2, cdf = imtools.histeq(im)

figure()
subplot(2, 2, 1)
axis('off')
gray()
title(u'原始图像', fontproperties=font)
imshow(im)

subplot(2, 2, 2)
axis('off')
title(u'直方图均衡化后的图像', fontproperties=font)
imshow(im2)

subplot(2, 2, 3)
axis('off')
title(u'原始直方图', fontproperties=font)
# hist(im.flatten(), 128, cumulative=True, normed=True)
hist(im.flatten(), 128, normed=True)

subplot(2, 2, 4)
axis('off')
title(u'均衡化后的直方图', fontproperties=font)
# hist(im2.flatten(), 128, cumulative=True, normed=True)
hist(im2.flatten(), 128, normed=True)

show()
```
  
路径：[直方图均衡](https://github.com/Heured/Assignment_01/blob/master/codes/zhiFangtuJunheng.py)

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/ZftJh.JPG)
  
## 高斯模糊
  
一个经典的并且十分有用的图像卷积例子是对图像进行高斯模糊。高斯模糊可以用于定义图像尺度、计算兴趣点以及很多其他的应用场合。  
  

  例：  
```python
 # -*- coding: utf-8 -*-
from PIL import Image
from pylab import *
from scipy.ndimage import filters

# 添加中文字体支持
from matplotlib.font_manager import FontProperties
font = FontProperties(fname=r"c:\windows\fonts\SimSun.ttc", size=14)

# im = array(Image.open('board.jpeg'))
im = array(Image.open('./data/image_forTest.jpg').convert('L'))

figure()
gray()
axis('off')
subplot(1, 4, 1)
axis('off')
title(u'原图', fontproperties=font)
imshow(im)

for bi, blur in enumerate([2, 5, 10]):
  im2 = zeros(im.shape)
  im2 = filters.gaussian_filter(im, blur)
  im2 = np.uint8(im2)
  imNum=str(blur)
  subplot(1, 4, 2 + bi)
  axis('off')
  title(u'标准差为'+imNum, fontproperties=font)
  imshow(im2)

# 如果是彩色图像，则分别对三个通道进行模糊
# for bi, blur in enumerate([2, 5, 10]):
#  im2 = zeros(im.shape)
#  for i in range(3):
#    im2[:, :, i] = filters.gaussian_filter(im[:, :, i], blur)
#  im2 = np.uint8(im2)
#  subplot(1, 4,  2 + bi)
#  axis('off')
#  imshow(im2)

show()
```
  
路径：[高斯模糊](https://github.com/Heured/Assignment_01/blob/master/codes/gaoSiMoHu.py) 

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/GaoSi_mohu.JPG)
  
## 高斯差分
  
图像强度的改变是一个重要的信息，被广泛用以很多应用中，正如它贯穿于本书中。  
  

  例：  
```python
# -*- coding: utf-8 -*-
from PIL import Image
from pylab import *
from scipy.ndimage import filters
import numpy

# 添加中文字体支持
from matplotlib.font_manager import FontProperties
font = FontProperties(fname=r"c:\windows\fonts\SimSun.ttc", size=14)

im = array(Image.open('./data/image_forTest.jpg').convert('L'))
gray()

subplot(1, 4, 1)
axis('off')
title(u'(a)原图', fontproperties=font)
imshow(im)

# Sobel derivative filters
imx = zeros(im.shape)
filters.sobel(im, 1, imx)
subplot(1, 4, 2)
axis('off')
title(u'(b)x方向差分', fontproperties=font)
imshow(imx)

imy = zeros(im.shape)
filters.sobel(im, 0, imy)
subplot(1, 4, 3)
axis('off')
title(u'(c)y方向差分', fontproperties=font)
imshow(imy)

#mag = numpy.sqrt(imx**2 + imy**2)
mag = 255-numpy.sqrt(imx**2 + imy**2)
subplot(1, 4, 4)
title(u'(d)梯度幅度', fontproperties=font)
axis('off')
imshow(mag)

show()
```
  
路径：[高斯差分](https://github.com/Heured/Assignment_01/blob/master/codes/gaoSiChaFen.py) 

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/GaoSi_chafen.JPG)
  
  
