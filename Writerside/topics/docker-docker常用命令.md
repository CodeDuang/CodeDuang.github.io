# [docker] docker常用命令


- 查看docker所有容器基本信息
```Bash
docker ps -a

# 查看容器ID(已知容器名)
docker ps -a | grep "[容器名]"
```

- 进入容器
```Bash
docker exec -it [容器名] bash 
```

- 停止容器
```Bash
docker stop [容器ID]
```

- 删除容器
```Bash
docker rm [容器ID]
```