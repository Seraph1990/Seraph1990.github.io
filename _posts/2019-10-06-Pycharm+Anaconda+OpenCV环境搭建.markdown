---
layout: post
title:  "Pycharm+Anaconda+OpenCV环境搭建"
description: 主要介绍了基于Anaconda下的OpenCV环境搭建，以及Pycharm配置
date:   2019-10-06 09:58:36
categories: Anaconda OpenCV
---
文|Seraph   
本文主要介绍了基于Anaconda下的OpenCV环境搭建，以及Pycharm配置。

### 01 | Ananconda安装
国外官网下载超慢，可以找国内镜像下载（但目前有很多国内镜像也不能下载了）
安装的话，默认点就行。（记得勾选添加环境变量）
如为勾选添加环境变量，请手动添加如下环境变量（以自己安装的目录为准）：
```
D:\Anaconda3
D:\Anaconda3\Scripts
D:\Anaconda3\Library\bin
```

### 02 | Ananconda配置OpenCV环境
1. 打开`Environment-base(root)`，右边下拉选项选择 `All`，然后搜索OpenCV
![OpenCV环境安装](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy80NTU3NjY1LTQ1MWZmZWJjMDgyNjZhNmYucG5n?x-oss-process=image/format,png)
勾选如上图三项，并点击界面右下角`Apply`（上图显示的是安装后的状态）。

### 03 | PyCharm安装
注意下载的是Community版本（用于Python语言开发）。

### 04 | 新建PyCharm工程
1. 新建PyCharm工程，然后在`Interpreter`中选择Ananconda中的Python环境即可。
![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy80NTU3NjY1LWY3NDk1M2U2MDJmOWRlMmIucG5n?x-oss-process=image/format,png)
2. 新建python文件，输入如下测试代码

```python
import cv2
import sys

if __name__ == "__main__”:
      #1.jpg为工程目录下的图片文件
     image = cv2.imread('1.jpg', cv2.IMREAD_ANYCOLOR)
     cv2.imshow("image", image)
     cv2.waitKey(0)
     cv2.destroyAllWindows()
```


### 05 | 可能遇到的一些问题
1. 用Anaconda Create Environments的时候，弹出`Multiple Errors Encountered`。   
解决：使用命令`conda create --name  scrapy python=3.7`创建。
2. conda install -c Anaconda opencv
