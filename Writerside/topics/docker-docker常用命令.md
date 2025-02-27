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