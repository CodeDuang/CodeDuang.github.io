# [docker] docker常用命令


## 查看容器基本信息
```Bash
docker ps -a

# 查看容器ID(已知容器名)
docker ps -a | grep "[容器名]"

#查看镜像
docker images
```

## 构建容器
```Bash
#在包含 Dockerfile 的目录中运行以下命令来构建镜像
docker build -t my_image_name .

#将根据当前目录中的 docker-compose.yml 文件启动服务
docker-compose up -d
```



## 进入容器
```Bash
docker exec -it [容器名] bash 
```

## 停止容器
```Bash
docker stop [容器ID]
```

## 删除容器or镜像
```Bash
#删除容器
docker rm [容器ID]

#删除镜像
docker rmi [镜像名]:[版本号]
```

## 添加用户到docker组 {#docker_1}
```Bash
# 查看当前用户所属所有组（输出如：user adm cdrom sudo dip plugdev lxd docker，第一个是用户名，后面是所属组，查看有没有docker）
groups
```
如果`groups`没有看到docker，则执行下面步骤，以添加docker组
```Bash
# 用户添加入docker组
sudo usermod -aG docker $USER
#usermod: 用于修改用户账户信息。
#-a: 将用户添加到组，而不从其他组中删除。
#-G: 指定要添加到的组（这里是 docker）。
#$USER: 你的用户名。你可以使用 $USER 环境变量来代替你的用户名
```
务必注意，现在使用`docker ps -a`依然是没有权限的，你还需要重启docker服务，并重进用户终端。
```Bash
#重启Docker服务
sudo systemctl restart docker
# or
sudo service docker restart
```
然后重新登录用户，此时使用`groups`就可以看到后面多了一个docker，同时`docker ps -a`也可以正常显示。


### 待研究（关于docker下载镜像总是会翻墙，奇哥给出的解法） {#docker_2}
```Bash
cat /usr/lib/systemd/system/docker.service

如果目标机器docker上无法使用梯子 可以设置本地某台机器的代理
[Unit]
Description=Docker Application Container Engine
Documentation=https://docs.docker.com
After=network-online.target docker.socket firewalld.service containerd.service time-set.target
Wants=network-online.target containerd.service
Requires=docker.socket


# for containers run by docker
#Environment="HTTP_PROXY=http://192.168.20.214:6152"
#Environment="HTTPS_PROXY=http://192.168.20.214:6152"
#Environment="NO_PROXY=localhost,127.0.0.1"
#Environment="ALL_PROXY=socks5://192.168.20.214:6153"



### 下一段
[service]
Type=notify
# the default is not to use systemd for cgroups because the delegate issues still
# exists and systemd currently does not support the cgroup feature set required
# for containers run by docker
#Environment="HTTP_PROXY=http://192.168.20.214:6152"
#Environment="HTTPS_PROXY=http://192.168.20.214:6152"
#Environment="NO_PROXY=localhost,127.0.0.1"
#Environment="ALL_PROXY=socks5://192.168.20.214:6153"
```
