# [Linux]开机自启设置

_（该方案适用于ubuntu系统，其他linux系统可以参考）_

在Linux系统中，默认`/etc/rc.local`文件作为开机自动执行用户命令的配置文件，
它是一个可执行脚本文件，系统启动时会自动运行它里面的命令（如果文件存在且可执行）。

所以可以将需要执行的命令放入`/etc/rc.local`，参考下面命令：
```Bash
# 使用vim编辑该文件（有可能系统中不存在该文件，新建即可）
vim /etc/rc.local 
```
`/etc/rc.local `内容参考：
```Bash
#!/bin/sh -e
# 这里写入需要执行的命令，例如输出测试信息
#如：cloudreve项目开机自启动
nohup /root/cloudreve/cloudreve > /root/cloudreve/output.log 2>&1 &

echo "开机自启动命令成功执行" > /root/auto_start.log

# 务必注意：所有开机自启命令，需要放在exit 0前！！！
exit 0
```

想要确认一下，上面操作是否有用，可以使用下面命令自启：
```Bash
reboot
```
