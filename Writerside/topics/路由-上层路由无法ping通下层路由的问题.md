# [路由]上层路由无法ping通下层路由的问题

参考博客：[上层路由无法ping通下层路由的问题](https://blog.csdn.net/qq_31856061/article/details/122921280)

今天想通过python -m http.server把本地的文件传给服务器时，发现服务器无法wget到。

本地ping了一下服务器，可以ping通；服务器ping本地，无法ping通。

通过问同事，才知道本地计算机和服务器在不同的路由器，本地计算机在下层路由器的子网中，服务器在上层路由器的子网中。
> **本地计算机的ip信息：**  
> 以太网适配器 以太网:  
连接特定的 DNS 后缀 . . . . . . . :  
本地链接 IPv6 地址. . . . . . . . : fe80::3068:dee7:7b98:c543%15  
IPv4 地址 . . . . . . . . . . . . : 192.168.60.145  
子网掩码  . . . . . . . . . . . . : 255.255.255.0  
默认网关. . . . . . . . . . . . . : 192.168.60.150  
>   
> **服务器的ip信息：**  
> eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500  
inet 192.168.2.100  netmask 255.255.255.0  broadcast 192.168.2.255  
inet6 fe80::67c:16ff:fe67:7fa0  prefixlen 64  scopeid 0x20<link>  
ether 04:7c:16:67:7f:a0  txqueuelen 1000  (以太网)  
RX packets 14938831  bytes 13633557788 (13.6 GB)  
RX errors 0  dropped 37860  overruns 0  frame 0  
TX packets 14306751  bytes 12898987300 (12.8 GB)  
TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0  
device interrupt 19  memory 0x9c100000-9c120000  

不清楚具体是什么情况，也无法解决，记录一下这个问题，期望后面可以解决。