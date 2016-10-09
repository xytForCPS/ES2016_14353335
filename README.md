#DOL配置实验
###**DOL框架描述**
DOL(distributed operation layer )是一种处理并行化程序的软件开发框架。
>The distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.

###**DOL安装笔记**
操作系统：linux虚拟机

1. 首先安装一些必要的环境
`$	sudo apt-get update
$	sudo apt-get install ant
$ 	sudo apt-get install openjdk-7-jdk
$	sudo apt-get install unzip`

2. 下载dol和systemc压缩包
直接用wget直接在虚拟机从源下载
`sudo wget http://www.accellera.org/images/downloads/standars/systemc/systemc-2.3.1.tgz
sudo wget http://www.tik.ee.ethz.ch/~shapes/downloads/dol_ethz.zip`
也可从主机拷贝安装包到虚拟机

3. 解压文件
* 新建dol的文件夹 
`$	mkdir dol`
* 将dolethz.zip解压到 dol文件夹中
`$	unzip dol_ethz.zip -d dol`
* 解压systemc
`$	tar -zxvf systemc-2.3.1.tgz`

4. 编译systemc
* 解压后进入systemc-2.3.1的目录下
`$	cd systemc-2.3.1`
* 新建一个临时文件夹objdir
`$	mkdir objdir`
* 进入该文件夹objdir
`$	cd objdir`
* 运行configure(能根据系统的环境设置一下参数，用于编译)
`$	../configure CXX=g++ --disable-async-updates`
如果运行configure的时候报错，可能是没有下载g++工具，安装g++即可
`$ sudo apt-get install gcc g++`
运行configure之后的结果截图：
！[查看图片](http://a3.qpic.cn/psb?/V11ttduT1jLeiZ/dIUR0XbNBPi.WzDgdREGwtC2Pj5UdhbCU3VOdudfMsM!/b/dAoBAAAAAAAA&bo=ewKSAAAAAAADB8k!&rf=viewer_4)
* 编译
`$	sudo make install`
查看编译后的文件目录如下：
！[查看图片](http://a3.qpic.cn/psb?/V11ttduT1jLeiZ/BW.BEh7groZ4FVev0udHeQvy5I1BJTtiW4BksSzQPZo!/b/dAoBAAAAAAAA&bo=eQKUAAAAAAADAMo!&rf=viewer_4)
记录当前工作路径:
`$ pwd`

5. 编译dol
* 进入刚刚dol的文件夹
`$	cd ../dol`
* 修改build_zip.xml文件
找到下面这段话
`<property name="systemc.inc" value="YYY/include"/>
<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>`
把YYY改成之前记录的systemc的工作路径
**这里需要注意，要检查之前的systemc编译后目录下是否有include和lib-linux两个文件夹，若没有，需要重新编译systemc。另外，对于64位系统的机器，可能生成文件名为lib-linux64而不是lib-linux，则改将这里的lib-linux改为lib-linux64**
* 编译
`$	ant -f build_zip.xml all`
若成功会显示build successful
* 接着可以试试运行第一个例子
进入build/bin/mian路径下
`$	cd build/bin/main`
然后运行第一个例子
`$	ant -f runexample.xml -Dnumber=1`
成功结果如图:
！[查看图片](http://a2.qpic.cn/psb?/V11ttduT1jLeiZ/qGiLDp26WxHRI4L4fdQMvuiOIrEw5aGsohDyhVAEVYg!/b/dAkBAAAAAAAA&bo=RAGIAQAAAAADAOk!&rf=viewer_4)


###**实验感想**
实验中遇到的最大的问题是，最后一步跑例子报错。后来发现，是build_zip.xml文件的编辑有问题，因为是64位操作系统，就把文件路径lib-linux改为lib-linux64，然后退回到systemc编译后的目录查看，实际生产的是lib-linux文件，把它改回来就跑成功了。。
