---
layout:     post
title:      使用DIGITS训练基于mnist数据集的手写数字识别模型
subtitle:   DIGITS的运行mnist实例
date:       2018-11-14
author:     PLlove
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - DIGITS
    - 数据集
    - 人工智能
---
# 使用DIGITS训练基于mnist数据集的手写数字识别模型

## 工作环境
确保已经安装好NVIDIA的DIGITS就行了。
## 介绍
本文将介绍如何使用DIGITS训练一个caffe模型，下面训练一个手写数字识别模型作为示例。使用[mnist手写数字数据库](http://yann.lecun.com/exdb/mnist/)作为数据集，使用DIGITS自带的LeNet作为模型。
## 下载数据集
直接在命令行中输入如下代码即可
```sh
python -m digits.download_data mnist ~/mnist
```
如果执行没问题就会显示
```sh
Downloading url=http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz ...
Downloading url=http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz ...
Downloading url=http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz ...
Downloading url=http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz ...
Uncompressing file=train-images-idx3-ubyte.gz ...
Uncompressing file=train-labels-idx1-ubyte.gz ...
Uncompressing file=t10k-images-idx3-ubyte.gz ...
Uncompressing file=t10k-labels-idx1-ubyte.gz ...
Reading labels from /home/username/mnist/train-labels.bin ...
Reading images from /home/username/mnist/train-images.bin ...
Reading labels from /home/username/mnist/test-labels.bin ...
Reading images from /home/username/mnist/test-images.bin ...
Dataset directory is created successfully at '/home/username/mnist'
```
如果运行出错，提示找不到download_data文件，那么很有可能是你没将digits根目录放到python环境变量中。
只需要将`/home/{你的用户名}/digits`放到`~/.bashrc/`的PYTHONPATH中就行了。
## 打开DIGITS服务
在DIGITS的根目录下输入`./digits-devserver`命令。看到类似于下面的代码说明启动成功。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114141159847.png)
## 将mnist导入DIGITS
打开浏览器键入`http://localhost:5000/`就能看到

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114141448541.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
点击右上角的login，输入一个你喜欢的名字，点击submit确认登录。
登陆后，我们就开始导入数据集。
点击Datasets，再点击images，弹出下拉菜单点击classification。
![在这里插入图片描述](https://img-blog.csdnimg.cn/2018111414183740.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
选择图像类型为灰度，大小为28*28，路径为/home/{你的用户名}/mnist/train，图像种类选png，名字MNIST。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114142109224.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
设置好后的样子，点击create开始导入数据集，等待工作完成。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114142612725.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
## 训练模型
数据集导入完成后，点击左上角的DIGITS，点击Models，再点击Images，弹出下拉菜单点击classification（与导入数据集时类似）。将各设置调整成下方的图片中的样子。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114143316230.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114143515474.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
设置完后，点击create开始训练模型，等待模型训练完成。
## 检测手写数字模型
训练完成后，模型的识别率基本能达到99%左右。训练完成后，如何查看效果呢？点击Browse选择一张手写数字图片，勾选Show visualizations and statistics，最后点击Classify One。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114144923847.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
在新弹出的标签页中你就能看见检测结果了，其中有每一层的图示，结构等各种信息。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145102374.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145126184.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145145720.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145205116.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145251558.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20181114145230583.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
参考文章：[DIGITS入门](https://github.com/NVIDIA/DIGITS/blob/master/docs/GettingStarted.md)
