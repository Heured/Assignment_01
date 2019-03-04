# Assignment_01
直方图、高斯滤波、直方图均衡  
  

原图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/image_forTest.jpg)
## 直方图
  
图像轮廓线和图线等高线。在画图像轮廓前需要转换为灰度图像，因为轮廓需要获取每个坐标[x,y]位置的像素值。  
  
路径: [直方图](https://github.com/Heured/Assignment_01/blob/master/codes/zhiFangtu.py)  

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/Zft.JPG)
  
## 直方图均衡
  
一个极其有用的例子是灰度变换后进行直方图均衡化。图像均衡化作为预处理操作，在归一化图像强度时是一个很好的方式，并且通过直方图均衡化可以增加图像对比度。  
  
路径：[直方图均衡](https://github.com/Heured/Assignment_01/blob/master/codes/zhiFangtuJunheng.py)

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/ZftJh.JPG)
  
## 高斯模糊
  
一个经典的并且十分有用的图像卷积例子是对图像进行高斯模糊。高斯模糊可以用于定义图像尺度、计算兴趣点以及很多其他的应用场合。  
  
路径：[高斯模糊](https://github.com/Heured/Assignment_01/blob/master/codes/gaoSiMoHu.py) 

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/GaoSi_mohu.JPG)
  
## 高斯差分
  
图像强度的改变是一个重要的信息，被广泛用以很多应用中，正如它贯穿于本书中。  
  
路径：[高斯差分](https://github.com/Heured/Assignment_01/blob/master/codes/gaoSiChaFen.py) 

效果图:  
![](https://github.com/Heured/Assignment_01/blob/master/imgs/GaoSi_chafen.JPG)
  
  
