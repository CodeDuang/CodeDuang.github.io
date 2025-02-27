# [venv]python虚拟环境

目前已知虚拟环境方案

## conda
- 介绍: 最常用的python管理工具，如果存储空间充足，非常推荐，除了占空间，不需要考虑其它毛病了

- 下载方法: 参考站内文档,[Experience]conda下载与自启配置

- 使用方法: 参考站内文档,[Experience]conda下载与自启配置

- 优点: 功能齐全

- 缺点: 臃肿，占空间

## venv
- 介绍: python自带的虚拟环境模块，不需要额外下任何东西。

- 下载方法: 不需要下载，python自带的模块。

- 使用方法: 
```Bash
#创建虚拟环境
python -m venv [虚拟环境名or路径] 

#启动虚拟环境
source 虚拟环境路径/bin/activate
```
- 优点: 方便快捷，轻量

- 缺点: 只能创建当前python的虚拟环境，如python3.7就只能创建python3.7的虚拟环境，无法创建3.8和3.9

### pyenv(不好用也没玩明白，不推荐)
- 介绍: 仅管理python版本，用来配合venv使用。

- 下载方法: 
```Bash
git clone https://gitee.com/mirrors/pyenv.git ~/.pyenv

#配置安装
vim ~/.bashrc
#把下面四行放入~/.bashrc末尾
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init --path)"
eval "$(pyenv init -)"
#保存退出，运行
source ~/.bashrc
```

- 使用方法: 
```Bash
#列出可用的 Python 版本
pyenv install --list

#安装一个特定版本的Python
pyenv install 3.9.9

#设置全局默认 Python 版本
pyenv global 3.9.9

#为当前目录设置局部 Python 版本
pyenv local 3.9.9

#查看当前 Python 版本
pyenv versions

#删除安装的某个 Python 版本
pyenv uninstall 3.9.9
```

- 优点: 方便快捷，轻量

- 缺点: 功能似乎不完善，（用的还不熟悉）。

## python uv(推荐)
- 介绍: 基于Rust构建的python package and project manager(python环境和项目的管理工具)，速度超快。

- 下载方法: 
```Bash
# On macOS and Linux.
curl -LsSf https://astral.sh/uv/install.sh | sh
 
# On Windows.
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```
- 使用方法:  
[官方文档](https://docs.astral.sh/uv/)  
[(博客园)Python包管理不再头疼：uv工具快速上手](https://www.cnblogs.com/wang_yb/p/18635441)
- 优点: 功能齐全，速度快，也能覆盖conda的功能

- 缺点: 新东西，需要学习（暂时没发现啥缺点）

```Bash
#python版本管理
uv python install #安装 Python 版本
uv python list #查看可用的 Python 版本
uv python find #查找已安装的 Python 版本
uv python pin #为当前项目指定使用的 Python 版本
uv python uninstall #卸载 Python 版本

#uv下载模块指定镜像源
uv add --default-index https://pypi.tuna.tsinghua.edu.cn/simple requests
```
