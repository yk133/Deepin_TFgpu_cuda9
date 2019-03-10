# 使用Deepin15.9安装tensorflow，cuda9+cudnn7.5+tf1.11
QwQ版本对照表查了资料几天，终于搞出来了。


### 1 在Deepi中切换显卡为Prime模式,自动安装显卡驱动，我目前默认是390.67，大于384，及格。
### 2 下载cuda9.0，cudnn对应版本(我是7.5)，按理说deb包应该安装更好更快，但是我发现我装上没什么用QwQ。
>2.1 安装cuda9 
>安装中如果你3s内被中断了.
       2.1.1 说是gcc版本不支持，就安装sudo apt install gcc-5,用软连接替换/usr/bin/gcc 到你的/usr/bin/gcc-5 【切记不要autoremove卸载现有的gcc 和g++】
       2.1.2 如果是缺库了，如libGUI.so， 就sudo apt install apt-file , sudo apt update,
      sudo apt-file search [缺失的文件]
       然后安装对应的包，注意一下，一般第一个就行了，但是如果你安装的时候要卸载某些包的话或者冲突，就不要装这个。


>2.2 复制cudnn里的内容:include和lib64复制到cuda下的include和lib64即可

### **3 环境变量的设置：**
sudo vim  /etc/profile
加到最后
``` 
# cuda9 && nvidia 这里cuda做了软连接到cuda-9.0 第二个非常重要，如果是用prime方案安装的显卡必须要有这个，否则很多包找不到！
export PATH=/usr/local/cuda/bin:$PATH
export PATH=$PATH:/usr/lib/x86_64-linux-gnu/nvidia/current
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

### 最后就安装pip3， sudo pip3 install tensorflow_gpu==1.11
[这里pip可以换成国内镜像源，具体可搜索]
然后在python3中import tensorflow或者网上找代码进行gpu测试和对比


>以上内容很多都是各种借鉴和踩坑后总结

