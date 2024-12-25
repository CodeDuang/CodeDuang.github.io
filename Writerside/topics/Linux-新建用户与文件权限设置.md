# [Linux]新建用户与文件权限设置

参考博客：

[linux 创建用户-博客园](https://www.cnblogs.com/flycc/p/14259969.html)
[【Linux基操】‘cat /etc/passwd‘命令解读](https://blog.csdn.net/Juryman155/article/details/135323931)
[Linux 使用 adduser 与 useradd 添加普通用户的正确姿势](https://p3terx.com/archives/add-normal-users-with-adduser-and-useradd.html)
## 第一步，useradd命令新建用户
输入如下命令(创建aa用户)：

```bash
useradd aa -d /home/aa -m -s /bin/bash
```

useradd 命令参数说明：

-d 指定用户目录
-m 创建用户目录
-s 指定shell命令工具，一般为/bin/bash

（如果想要检查创建成功没有可以使用命令：`cat /etc/passwd`，查看账户信息，看不懂的话可以参考[Linux 使用 adduser 与 useradd 添加普通用户的正确姿势](https://p3terx.com/archives/add-normal-users-with-adduser-and-useradd.html)的解释）
## 第二步，passwd命令设置密码
输入如下命令(为aa用户设置登录密码)：

```bash
passwd aa
```
然后再输入两次设置的密码就可以了
（注意，这种方式生成的用户只有自己文件夹/home/aa的控制权限，无法修改其它文件夹的内容）

## 补充：文件权限设置
格式：
```bash
chmod 777 -R [文件夹绝对路径]
```
chmod为权限指令，777为权限情况（所有人都可以读写删），-R指定了该文件夹包括子文件夹
例：

```bash
chmod 777 -R /home/miniconda3
```
查看当前目录下文件夹权限情况：
```bash
ls -l
```
效果如图:

![image_23.png](image_23.png)