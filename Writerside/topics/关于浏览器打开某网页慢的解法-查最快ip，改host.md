# 关于浏览器打开某网页慢的解法(查最快ip，改host)

参考博客： [CSDN 访问慢解决办法 ](https://www.cnblogs.com/FCmmmmmm/p/16040389.html)

### F12打开网络工具

以打开csdn网页为例，首先按下F12,然后Ctrl+R重新加载网页。

在“网络”菜单下，可以看到网页的实时加载情况，发现xxx.png竟然加载了4分钟。
![image_42.png](image_42.png)

### 查域名，本地ping一下

![image_43.png](image_43.png)

上面图片发现这个加载了4分钟的资源，来自：csdnimg.cn

本地ping一下，果然请求超时
![image_44.png](image_44.png)

### 进站长工具找该域名对应最快的ip节点

[站长工具](https://ping.chinaz.com/)

把域名输入，找到最快节点

![image_45.png](image_45.png)

### 存入host
![image_46.png](image_46.png)

这里最快的ip的是：140.249.149.9

打开windows的host文件(linux的host百度一下嗷)，路径在：C:\Windows\System32\drivers\etc

编辑host，添加如下行：

140.249.149.9    csdnimg.cn

![image_47.png](image_47.png)

重启浏览器，刷新DNS