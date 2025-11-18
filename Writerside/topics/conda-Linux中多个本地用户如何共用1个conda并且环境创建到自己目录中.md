# [conda]Linux中多个本地用户如何共用1个conda并且环境创建到自己目录中

_针对于linux新建用户，但不想让新建用户自己下载conda，已有的conda新建用户没有权限自由的创建环境。_

### 解决方案原理

新建用户虽然没有其它用户conda的写和修改的权限，但是对conda有读取的权限。

可以设置一系列环境变量，将conda的所有新环境、下载的包缓存、自己编译都设置到自己的目录中。

这样只需要借用其它用户的conda新建自己的环境即可

### 步骤1：登录自动运行conda脚本

##### 完整版：新增如下脚本到~/.bashrc  

_请注意，使用`vim ~/.bashrc`编辑文件，将`/home2/lbj/miniconda3/bin/conda`路径修改为实际服务器中conda所在路径_

```Bash
__conda_setup="$('/home2/lbj/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home2/lbj/miniconda3/etc/profile.d/conda.sh" ]; then
        . "/home2/lbj/miniconda3/etc/profile.d/conda.sh"
    else
        export PATH="/home2/lbj/miniconda3/bin:$PATH"
    fi
fi
unset __conda_setup
```
第一行：运行 conda shell.bash hook，conda 会实时吐出一段 专门针对当前用户、当前安装路径 的 bash 函数/别名。

第一个if：用 eval 直接载入，速度最快、兼容性最好。

else:  回退方案：老版本或钩子失败时

else中第一个if： 找不到钩子就 source 旧的 conda.sh（同样能注册 conda activate）。

else中else：如果连 conda.sh 都没有，最差仅把 bin 目录塞进 PATH，至少能用 conda create/install/list，但 activate 会失效。

最后一行：清理变量

##### 简单速成版：新增如下脚本到~/.bashrc {#bashrc_1}
```Bash
__conda_setup="$('/home2/lbj/miniconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
[ $? -eq 0 ] && eval "$__conda_setup"
unset __conda_setup
```

### 步骤2：设置自己用户的系统conda变量,新增如下脚本到~/.bashrc

```Bash
export CONDA_ENVS_PATH=$HOME/.conda/envs      # 所有新环境落到这里
export CONDA_PKGS_DIRS=$HOME/.conda/pkgs      # 下载的包缓存
export CONDA_BLD_PATH=$HOME/conda-bld         # 以后自己编译也放这里
```

### 步骤3：刷新一下~/.bashrc

```Bash
source ~/.bashrc
```
此时，应该出现了base环境，但base环境由于属于其它用户，所以需要使用`conda create -n [new_env_name]`新建自己的环境，
后续切换到自己的环境即可正常下载包。





