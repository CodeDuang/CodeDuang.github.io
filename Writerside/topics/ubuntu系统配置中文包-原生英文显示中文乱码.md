# ubuntu系统配置中文包(原生英文显示中文乱码)

参考博客：
[1][ubuntu 配置 locale（语言环境）](https://blog.csdn.net/ymz641/article/details/131607024)

在新装的ubuntu系统上，由于系统默认使用的是英文语言包，所以任何带有中文的文件名或内容会显示乱码，需要更改系统语言为中文来解决

## 1.locale命令查看当前系统语言设置
命令如下:
```bash
locale
```

![image_11.png](image_11.png)

发现字符集设置的都是en_US.UTF-8，这种字符集没有中文编码，所以中文显示出来是乱码。
## 2.locale -a 命令，查看当前可切换的字符集
命令如下：
```bash
locale -a 
```

![image_12.png](image_12.png)

我安装了中文的字符集，所以有上图的最后两行，一般来讲ubuntu系统不自带zh_CN.utf8字符集的，下一步就是安装zh_CN.utf8字符集，已经有的可以跳过。

## 3.安装zh_CN.utf8字符集
### 3.1.下载language-pack-zh-hans
```bash
sudo apt install language-pack-zh-hans
```

![image_13.png](image_13.png)

首先下载language-pack-zh-hans，这个包里面有各个语言的字符集，我这边已经下好了language-pack-zh-hans

### 3.2.设置/etc/locale.gen
```bash
vim /etc/locale.gen
```
进入这个文件，一滑到底，将zh_CN.UTF-8 UTF-8一行解开注释（需要按i键进入编辑模式）。

![image_14.png](image_14.png)

（解开注释后，按Esc键，再输入`:wq`，就可以保存并退出了）

```bash
 sudo locale-gen
```
使用上面命令，就可以把解注释的字符集进行安装了

![image_15.png](image_15.png)

```bash
locale -a 
```

![image_16.png](image_16.png)

再看看系统可切换的字符集，发现zh_CH.utf8已经在里面了。

## 4.切换系统字符集为zh_CN.utf8

编辑/etc/profile，在最后新增两行代码：
export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:zh
命令如下:
```bash
sudo vim /etc/profile
```

![image_17.png](image_17.png)

（我是在最开头加的，不影响）


运行/etc/profile，命令如下：
```bash
source /etc/profile
```

![image_18.png](image_18.png)

再用locale查看一下系统字符集

```bash
locale
```

![image_19.png](image_19.png)

（切换成功，教程结束，打开一个中文文档，发现中文已经能够正常显示了）

![image_20.png](image_20.png)
