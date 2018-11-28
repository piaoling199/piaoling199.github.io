---
layout:     post
title:      Jetson TX2/1 在编译caffe-0.15时报错处理方案
subtitle:   Jetson TX系列安装caffe时报错处理
date:       2018-11-16
author:     PLlove
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - TX2
---
# Jetson TX2/TX1 在编译caffe-0.15时报错处理方案
## 报错内容
在TX1或TX2上编译caffe-0.15时，出现如下错误：
```sh
/tmp/ccEiMrO7.s: Assembler messages:
/tmp/ccEiMrO7.s:1533: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:1857: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:2204: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:2679: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:4226: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:5069: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:5320: Error: unknown mnemonic pause' --pause'
/tmp/ccEiMrO7.s:5441: Error: unknown mnemonic pause' --pause'
src/caffe/CMakeFiles/caffe.dir/build.make:650: recipe for target 'src/caffe/CMakeFiles/caffe.dir/util/gpu_memory.cpp.o' failed
make[2]: *** [src/caffe/CMakeFiles/caffe.dir/util/gpu_memory.cpp.o] Error 1
CMakeFiles/Makefile2:272: recipe for target 'src/caffe/CMakeFiles/caffe.dir/all' failed
make[1]: *** [src/caffe/CMakeFiles/caffe.dir/all] Error 2
Makefile:127: recipe for target 'all' failed
make: *** [all] Error 2
```
## 解决方案

找到 `$CAFFE_ROOT/3rdparty/cub/host/mutex.cuh`文件，将124行左右的
```sh
 --- #ifndef __arm__
```
改成
```sh
+++ #if !defined(__arm__) && !defined(__aarch64__)
```
即可。
在编译一遍应该就没问题了。
```sh
make clean && make -j4
```
参考文章：[NVIDIA DEVELOPER 论坛（The problem with the assembly of caffe-0.15 on JetsonTX1）](https://devtalk.nvidia.com/default/topic/976063/?comment=5016412)
