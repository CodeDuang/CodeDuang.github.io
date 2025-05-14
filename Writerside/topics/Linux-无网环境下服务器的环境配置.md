# [Linux]无网环境下服务器的环境配置

背景：局域网有一台无法访问互联网的linux服务器，和自己能够上网的window系统笔记本(笔记本安装好了wsl)。
现在的需求是想通过服务器跑一些程序，但是服务器本身无法访问互联网下载文件(自己电脑下好传过去就好了)配置环境(本章内容)，
于是尝试使用自己的笔记本帮助服务器完成环境配置。

###  步骤0：装wsl（已经有的可以跳过）
使用管理员权限打开cmd，然后使用命令：`wsl --install -d Ubuntu`
![image_60.png](image_60.png)

安装好了，重启电脑，配个账号密码就可以使用了。

### 方法1：使用python自带的venv工具(miniconda做python版本管理)，在wsl中完成环境配置后，传给Linux服务器
#### 1.1.笔记本上，miniconda安装包下载
下载miniconda的linux安装包：[repo.anaconda.com](https://repo.anaconda.com/miniconda/)
![image_59.png](image_59.png)

#### 1.2.笔记本上，miniconda安装包放到合适路径
直接在文件管理器的路径中输入`linux`就可以进入wsl的路径了，如下图：
![image_61.png](image_61.png)

下载好的miniconda安装包找个路径拖进去就好了：
![image_62.png](image_62.png)

#### 1.3.笔记本上，启动wsl，进入对应路径，安装miniconda

使用`bash`命令
![image_63.png](image_63.png)

安装完毕重新启动一次wsl(或者使用`source ~/.bashrc`命令)，就进入conda环境中了
![image_65.png](image_65.png)

#### 1.4. 笔记本的wsl中，创虚拟环境

使用`python -m venv .venv`在当前目录下创建一个虚拟环境
![image_64.png](image_64.png)
(注意，使用`ll`命令可以看到“.venv”,使用`ls`无法看到)

进入这个虚拟环境(不用conda的虚拟环境，里面可能有一些依赖conda的东西)
```bash
conda deactivate #退出conda环境

source .venv/bin/activate #进入python自带模块造出来的.venv虚拟环境(注意路径)
```
![image_66.png](image_66.png)

试着随便安装一些python模块，等下打包到服务器上进行可用性验证(比如numpy)
![image_67.png](image_67.png)

#### 1.5.连接服务器，上传虚拟环境（出现了不识别的问题，待解决）

打开项目路径(如下)
![image_68.png](image_68.png)






