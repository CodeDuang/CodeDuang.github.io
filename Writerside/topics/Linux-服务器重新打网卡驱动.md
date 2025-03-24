# [Linux]服务器重新打网卡驱动

适用场景：linux服务器原本网卡驱动正常，突然掉网卡驱动的情况（即驱动已经下载好了）

#### 查看服务器中已加载模块是否有网卡驱动

```Bash
#本服务器的网卡驱动为e1000e,不同服务器请自行调整
lsmod | grep e1000e 
```
![image_48.png](image_48.png)

发现无输出，说明网卡驱动已经没有工作了

#### 尝试运行网卡驱动内核

```Bash
# 打上e1000e驱动，其它驱动请自行更改名称
sudo modprobe e1000e
```
![image_49.png](image_49.png)

加载内核的命令没有报错，再使用`lsmod | grep e1000e`检查是否加载成功。（图中成功了）

#### 查看系统中与网络相关的 PCI 设备信息

```Bash
lspci | grep net
#输出可能如下：（表示系统中有一个以太网控制器（Ethernet controller）和一个无线网络控制器（Network controller））
#00:03.0 Ethernet controller: Intel Corporation Ethernet Connection (3) I218-LM (rev 03)
#01:00.0 Network controller: Broadcom Inc. and subsidiaries BCM4360 802.11ac Wireless Network Adapter (rev 03)
```

#### 查看网络参数

```Bash
ifconfig
```
![image_50.png](image_50.png)

发现没有ip地址，所以还需要配置一下ip地址

#### 给网卡配置ip和子网掩码

```Bash
#格式
sudo ifconfig [网卡名] [配置ip] netmask [子网掩码]
#例
sudo ifconfig en1 192.168.1.28 netmask 255.255.255.0

```

此时使用`ifconfig`可能还是无法查看到ip的显示，需要重启网络服务。

#### 重启网络服务

```Bash
# 两个命令二选一
sudo systemctl restart network
# 或
sudo systemctl restart NetworkManager
```
此时再使用`ifconfig`发现已经有ip了，问题解决

![image_51.png](image_51.png)


#### （未完待续...）后续发现，不管接入哪个局域网，使用`ifconfig`显示的ip和子网掩码都不变，且无法和其它设备互相ping通