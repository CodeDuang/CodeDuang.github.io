# [Linux]常用命令合集


```Bash
# 统计当前目录下有多少个文件

ls -l | grep "^-" | wc -l
```

```Bash
# 获取内存情况

free -h
```

```Bash
# 获取磁盘挂载情况

df -h
```

```Bash
# 获取当前目录占用硬盘空间大小

#返回当前目录大小
du -sh
#列出目录下各个文件和文件夹的大小
du -sh *
```

```Bash
# 检测ip端口的开放情况

nc -vz [ip] [port]
#上面是格式，下面是举例
nc -vz 127.0.0.1 22
nc -vz 8.137.124.187 7002
```
<procedure title="解释：" id="inject-a-procedure">
    <p><shortcut>nc</shortcut>：netcat 的缩写，是一个强大的网络工具，可以进行网络连接、端口扫描、数据传输等。</p>
    <p><shortcut>-v</shortcut>：启用详细模式（verbose），会输出更多信息，比如连接尝试的状态。</p>
    <p><shortcut>-z</shortcut>：启用扫描模式（zero I/O mode），不发送数据，只尝试建立连接，主要用于端口扫描。</p>
</procedure>

```Bash
# 解压

#zip解压命令
unzip [zip文件名]
#.tar解压命令
tar -xf [文件名]
#.tar.gz解压命令
tar -xzf [文件名]
```

```Bash
# 压缩

#不压缩，仅归档（.tar）([file1] [file2] ...表示可以压缩多个文件或者仅1个文件)
tar -cf  [压缩包名.tar] [file1] [file2] ...
#gzip压缩（.tar.gz）
tar -czf [压缩包名.tar.gz] [file1] [file2] ...
```

```Bash
# 生成venv虚拟环境

#前提是已经在一个python环境下，想要额外针对项目生成一个虚拟环境
pyhon -m venv [路径+文件名]
#举例（不给路径，表示就在命令所在路径生成虚拟环境）
pyhon -m venv .venv
pyhon -m venv /home/yc/yolov8/.venv
```

```Bash
# 使用python起一个局域网http文件服务

#指定目录+端口
python -m http.server 8080 --directory /path/to/your/directory
#简单版，默认在命令目录开8000端口
python -m http.server
```

```Bash
查看系统和内核信息

hostnamectl
```
```Bash
查看服务器内存

free -h
```
    
