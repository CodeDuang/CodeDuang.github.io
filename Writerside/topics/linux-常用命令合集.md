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
# 查看系统和内核信息

hostnamectl
```
```Bash
# 查看服务器内存

free -h
```

```Bash
# 输出文档末尾几行信息（常用来查日志信息）（还有更多可扩展的东西，如和cat结合以及输出特定行数，请后续再探索）
tail [文件名]
# 举例
tail output.log
```

```Bash
# 使用scp命令，跨服务器复制文件(可以上传，可以下载，但是有密码的话，得手动输入，想要自动化得用密钥的方式)

#一般是从远程服务器拷贝对应目录的文件下来
scp -P [远程服务器端口号] [登录用户名]@[公网ip]:/文/件/夹/路/径/文件名.xyz [本地路径]
# 举例(下载服务器特定路径的a.onnx到本地当前目录)
scp -P 2228 root@123.123.123.123:/home/root/a.onnx ./

# 如果是目录拷贝（包含子目录子文件一起拷贝，可以使用参数: -r）
scp -r -P 2228 root@123.123.123.123:/home/root/ ./



```
    
