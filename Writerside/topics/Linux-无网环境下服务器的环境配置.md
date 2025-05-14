# [Linux]无网环境下服务器的环境配置

背景：局域网有一台无法访问互联网的linux服务器，和自己能够上网的window系统笔记本(笔记本安装好了wsl)

###  步骤0：装wsl（已经有的可以跳过）
使用管理员权限打开cmd，然后使用命令：`wsl --install -d Ubuntu`
![image_60.png](image_60.png)
重启

### 方法1：使用python自带的venv工具，在wsl中完成环境配置后，传给Linux服务器
#### 1.1.在笔记本中的wsl里安装conda进行python版本管理

下载miniconda的linux安装包：[repo.anaconda.com](https://repo.anaconda.com/miniconda/)
![image_59.png](image_59.png)

