# git疑难杂症与命令

## git清除缓存+忽略上传文件 {id="git_1"}
### 清除缓存
```Bash
#这种会清除本地所有的git add . 和 git commit -m "" 的东西
git rm -rf . --cached
#随时可以查看一下日志
git log
```
### 忽略上传（管理本地和github文件） {id="github_1"}
```Bash
#创建.gitignore文件
touch .gitignore
#把不想上传到远程仓库的文件名传入.gitignore
echo ".idea" > .gitignore
```

## github空仓库，直接上传本地项目
```Bash
git remote add origin git@github.com:CodeDuang/blog_old_file.git
git branch -M main
git push -u origin main
```
## 其它git疑难杂症与命令
### 本地文件初始化为仓库(git switch --create main)：
```Bash
git init --initial-branch=main
```


### 配置用户和邮箱：
```Bash
git config --global user.name "言辰寸心"
git config --global user.email "2962402977@qq.com"
```

### 设置上传和拉取对应的仓库地址
```Bash
git remote add origin git@gitlab.com:codexie/test1.git
```

### 拉取远程仓库代码（--allow-unrelated-histories 允许没有共同历史记录的分支合并）：
```Bash
git pull origin main
```

### 常规上传
```Bash
git add .
git commit -m "上传"
git push --set-upstream origin main
```




# 解决问题
测试是否正常连接（github可以换为gitlab）：
ssh -T git@github.com


本地生成密匙（注意最后的邮箱，可填自己邮箱）：
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

本地选择密钥路径
ssh-add ~/.ssh/id_rsa

检查SSH Agent服务状态（略）