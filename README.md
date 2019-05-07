LargeImageDetect-yolo-windows
===============
修改yolo-windows源码[![HUAWEI](https://img.shields.io/badge/link-Darknet-blue.svg)](https://github.com/AlexeyAB/darknet)，添加高分辨率图像分割检测代码，可封装为lib,dll方便移植，提供模型实现航拍车辆检测，其中模型训练在Ubuntu下完成，应用在Windows下。

项目要点
--------
* 采用滑窗裁剪存入文件夹，再送入yolov3，实现超大图检测。
	* 如若修改滑窗步长及分割大小
		* 修改cutAndSace.h

		```C++
		#define CUTWID 512
		#define CUTHEI 512
		#define CUTSTEP 512
		```
		* 修改image.c
		```C++
		#define CUTSTEP 512
		```	
	* 如若修改保存文件夹
		* 修改darknet.c

		```C++
		//Save
		char dirPath[] = "x64\\data\\testSplit\\";
		char imgSrcFilename[] = "x64\\data\\panorama.jpg";
		```		
* 将终端操作修改为测试文件夹，可以实现自动测试
	* 如若修改测试文件夹
		* 修改darknet.c
		
		```C++
		//Test
		char filename[] = "x64\\data\\testSplit";
		```
* 可以将代码封装为lib,dll，方便移植
* 模型只用来检测航拍车辆，下载后放入build\darknet\x64文件夹下
* 运行显示多幅图，最后一张为超大图检测效果，若不显示中间图，修改detector.c中run_detector

```C++
int dont_show = 1;
```

模型测试
--------
* 提取码：gqnv，模型下载[![HUAWEI](https://img.shields.io/badge/DownLoad-Model-green.svg)](https://pan.baidu.com/s/18r_Vj5jstC--yfBmDrB_xw)
* 航拍高度为100m，只检测车辆

<div align=center><img width="400" height="382" src="https://github.com/qinguoyi/yolo-windows/blob/master/result/100_1.png"/></div> 

环境配置
--------
* VS2013+OpenCV3.1+CUDA8.0+CUDNN5.1
* Intel i7 7700 + GTX1070下检测时间30-40ms per img

More Details
-------------
Ubuntu下模型训练请访问[![HUAWEI](https://img.shields.io/badge/Ubuntu-ModelTrain-red.svg)](https://www.cnblogs.com/qinguoyi/p/8507803.html)，Windows下滑窗处理请访问[![HUAWEI](https://img.shields.io/badge/Windows-SlideProcess-orange.svg)](https://www.cnblogs.com/qinguoyi/p/9983858.html)
