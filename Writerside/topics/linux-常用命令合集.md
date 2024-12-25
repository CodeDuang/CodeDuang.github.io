# [linux]常用命令合集


1. 统计当前目录下有多少个文件
```Bash
ls -l | grep "^-" | wc -l
```

2. 获取内存情况
```Bash
free -h
```

3. 获取磁盘挂载情况
```Bash
df -h
```

4. 获取当前目录占用硬盘空间大小
```Bash
#返回当前目录大小
du -sh
#列出目录下各个文件和文件夹的大小
du -sh *
```

5. 检测ip端口的开放情况
```Bash
nc -vz [ip] [port]
#上面是格式，下面是举例
nc -vz 127.0.0.1 22
nc -vz 8.137.124.187 7002
```
解释：
- nc: netcat 的缩写，是一个强大的网络工具，可以进行网络连接、端口扫描、数据传输等。
- -v: 启用详细模式（verbose），会输出更多信息，比如连接尝试的状态。
- -z: 启用扫描模式（zero I/O mode），不发送数据，只尝试建立连接，主要用于端口扫描。

6. 压缩包解压
```Bash
#zip解压命令
unzip [zip文件名]
#.tar解压命令
tar -xf [文件名]
#.tar.gz解压命令
tar -xzf [文件名]
```

7. 压缩包压缩
```Bash
#不压缩，仅归档（.tar）([file1] [file2] ...表示可以压缩多个文件或者仅1个文件)
tar -cf  [压缩包名.tar] [file1] [file2] ...
#gzip压缩（.tar.gz）
tar -czf [压缩包名.tar.gz] [file1] [file2] ...
```
