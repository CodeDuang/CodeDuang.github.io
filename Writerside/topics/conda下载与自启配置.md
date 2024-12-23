# conda下载与自启配置
*注意：该博客由于是很早之前写的，现在回顾，稍有粗糙*

Linux启动时读取配置文件的顺序: [https://blog.csdn.net/fengyuyeguirenenen/article/details/133978944](https://blog.csdn.net/fengyuyeguirenenen/article/details/133978944)

首先，新建的用户是没有各个文件夹的读写权限的，为了防止该新建用户扰乱别人的conda环境，遂不打算给新建用户开放公共的conda权限，可以在该用户的目录下`/home/newuser`给他单独搞一个conda环境。

### 1.下载conda
miniconda官网：[https://docs.anaconda.com/free/miniconda/](https://docs.anaconda.com/free/miniconda/)，点击下图红色部分下载安装包

![image_24.png](image_24.png)

下载后，传入linux服务器中，然后依次输入下面的命令(注意:Miniconda3-latest-Linux-x86_64.sh根据自己下载的conda安装包修改为对应的名字)：

```bash
bash Miniconda3-latest-Linux-x86_64.sh -b -u -p ~/miniconda3
rm -rf Miniconda3-latest-Linux-x86_64.sh
```

再执行下面命令，将conda启动写入bash。

```bash
~/miniconda3/bin/conda init bash
~/miniconda3/bin/conda init zsh
```

*重启，如果此时发现conda还是没有被启动，就需要用到root账户了（见下面）。*

![image_25.png](image_25.png)

首先需要使用root用户将`/etc/bashrc`复制给用户的`~/.bashrc`，然后尝试source命令激活一下，看看会不会自动在用户目录下`/home/newuser`生成conda文件。

### 2.查看~/.bashrc并编辑
使用新建用户登录linux服务器，输入下面命令编辑~/.bashrc：

```bash
vim ~/.bashrc
```
如下图，各个路径都是以`/home/newuser`开头的，说明conda的下载和启动都从该路径开始。

![image_26.png](image_26.png)

按键盘上的`i`是编辑模式
编辑结束了按`Esc`,再输入`:wq`保存并退出


### 3.加载~/.bashrc
退出bashrc文件后，输入如下命令，启动~/.bashec
```bash
source ~/.bashrc
```

![image_27.png](image_27.png)

如果用户前面突然多了个（base），说明成功了。
但你会发现，每次重启都需要输入一下启动~/.bashrc的命令。（一般来讲不需要，每次登录账号进入服务器的时候，会自动运行该用户的~/.bashrc）
这是因为，linux启动时并没有自动运行~/.bashrc。

### 4.根据Linux启动时读取配置文件的顺序原理，运行~/.bashrc

原理请参考： [https://blog.csdn.net/fengyuyeguirenenen/article/details/133978944](https://blog.csdn.net/fengyuyeguirenenen/article/details/133978944)

![image_28.png](image_28.png)

这边我直接在~/.bash_profile中加入了如下信息

```bash
scoure ./bashrc
```
如图：

![image_29.png](image_29.png)

保存退出后，使用`source ~/.bash_profile`命令，发现确实可以通过~/.bash_profile启动 ~/.bashrc。
重启，发现解决问题（每次重启都需要输入一下启动~/.bashrc的命令）了。