---
title: linux下使用gcc编译so库
date: 
update:
tags: 
- so库
- gcc
category: linux
---
最近公司在做微信端的定位和导航，所以需要云端提供导航和定位功能，为了复用之前客户端的代码，所以我需要把c文件编译成linux下可以运行的so库，记录一下过程。

<!-- more -->
由于没有搞过，所以遇到问题也不知道具体是哪里的问题，所以就一路乱试。。。最后试了下，可以用。

### 用到的一些gcc命令
> -shared:指定生成动态连接库,不用该标志外部程序无法连接。相当于一个可执行文件(我开始没加这个，报错找不到main)
> 
> -fPIC:表示编译为位置独立的代码，不用此选项的话编译后的代码是位置相关的所以动态载入时是通过代码拷贝的方式来满足不同进程的需要，而不能达到真正代码段共享的目的。
> 
> -I:指定头文件所在的文件夹

### 遇到的问题
#### 编译时报错：找不到jni.h
我用虚拟机装了Ubuntu，输入java没有找到，然后按着提示随便装了一个。。。
当然我现在知道装的是OpenJDK([OpenJDK和SunJDK的区别](https://www.zhihu.com/question/19646618))，google也决定在android N中使用OpenJDK了([相关报道](http://www.infoq.com/cn/news/2016/01/android-openjdk))。。

所以我又下载了SunJDK，编译的时候要引用相关文件,加如下命令

	 -I/[jdk目录]/include -I/[jdk目录]/include/linux
[jdk目录]/include是jni.h所在目录；
[jdk目录]/include/linux是jni_md.h所在目录
#### 编译报错：找不到main
没有加命令 -shared(命令介绍参考上面)
		
#### 编译时报错：找不到math.h
使用math.h中声明的库函数，gcc命令行必须加-lm选项，因为数学函数位于libm.so库文件中（这些库文件通常位于/lib目录下），-lm选项告诉编译器，我们程序中用到的数学函数要到这个库文件里找。

我最后是把c文件一个一个编译成.o然后，然后在编译成.so的，因为怕出错，不知道哪个文件的问题。。。当然也可以直接一句话如下：

	gcc [.c文件，多个用空格隔开] -fPIC -shared -I/usr/xxx/include -I/usr/xxx/include/linux -lm -o libtest.so
	
编译成.o命令:gcc -c test.c

.o编译成.so:gcc test.o -o test(默认会添加lib前缀和.so后缀)