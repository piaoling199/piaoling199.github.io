---
layout:     post
title:      TX1/TX2上快捷部署TensorFlow
subtitle:   TX2新手的TensorFlow福音
date:       2018-11-19
author:     PLlove
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - TX2
    - TensorFlow
---
# TX1/TX2上快捷部署TensorFlow
对所有想要学习TensorFlow的人来说，环境安装是入门的第一个坎。网络上已经有非常多的安装教程，但总是会有这样或那样的让人头大的情况发生，运气好的话，百度一下就解决了，否则就有得折腾了。今天给使用NVIDIA TX1/TX2开发板的伙伴们带来一波福利，就如标题所说的快捷部署TensorFlow。
## 方法一
直接命令行运行下面代码即可。不过不知道为什么有时候报错，暂未找到解决方案。报错的伙伴用方法二吧。
```sh
pip install --extra-index-url=https://developer.download.nvidia.com/compute/redist/jp33 tensorflow-gpu
```
## 方法二
#### 第一步
下载你所需要的包，[地址](https://github.com/peterlee0127/tensorflow-nvJetson/releases)。我安装的是1.9.0版python2.7的TensorFlow，如下图。![在这里插入图片描述](https://img-blog.csdnimg.cn/20181119145315279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzY0MDM2OQ==,size_16,color_FFFFFF,t_70)
#### 第二步
用pip安装下载好的包就行了，等待安装完成就大功告成了。
```sh
pip install tensorflow-1.9.0-cp27-cp27mu-linux_aarch64.whl
```
