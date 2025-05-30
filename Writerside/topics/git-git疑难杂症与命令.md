# [git]git疑难杂症与命令

## 1.身份认证 {id="1."}
_(所有远程仓库代码同步大前提，上传和同步的各种权限错误大概是这个步骤没做)_ 

第一步：本地git交互窗口生成密匙（注意最后的邮箱，可填自己邮箱）：
```Bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```
![image_69.png](image_69.png)

第二步：根据提示路径(红色部分，可以自己设置)复制后缀为.pub的文件内容。

![image_70.png](image_70.png)

第三步：打开自己的github，在个人头像下面选择：

![image_71.png](image_71.png)

## 2.git连接远程仓库流程 {id = "git_1"}
### 情况1：远程仓库为空，本地仓库不为空，上传代码
```Bash
# 确定远程仓库
git remote add origin git@github.com:CodeDuang/blog_old_file.git

# 确定身份
git config --global user.name "言辰寸心"
git config --global user.email "2962402977@qq.com"

# 确定分支
git branch -M main

# 仓库同步到本地
git pull origin main

# 上传一条龙(强制上传，请务必确保远程仓库没有重要内容)
git add .
git commit -m "init"
git push -u origin main --force 
```

## 3.git常用命令 {id="git_2"}
### 初始化仓库
```Bash
git init
```

### git清除缓存+忽略上传文件  {id="git_3"}
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
# 确定远程仓库
git remote add origin git@github.com:CodeDuang/blog_old_file.git

# 确定身份
git config --global user.name "言辰寸心"
git config --global user.email "2962402977@qq.com"

# 确定分支
git branch -M main

# 仓库同步到本地
git pull origin main

# 上传一条龙(强制上传，请务必确保远程仓库没有重要内容)
git add .
git commit -m "init"
git push -u origin main --force 
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

## ssh-agent

```Bash
# 报错如下(系统无法连接到ssh-agent)
Could not open a connection to your authentication agent.

# 解决方法：启动 SSH 代理
eval "$(ssh-agent -s)"
```

## 权限拒绝
1.本地生成密匙（注意最后的邮箱，可填自己邮箱）：
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

2.本地选择密钥路径
ssh-add ~/.ssh/id_rsa

3.在github自己的账号里面，添加id_rsa.pub中内容到令牌中，以方便令牌验证登录（注意，github只允许通过令牌登录git以同步仓库信息）
![image_58.png](image_58.png)

（理论上此时就可以进行访问了，如果还是权限拒绝，那就使用`ssh-add "D:\blog\.ssh\id_rsa"`指定本地对应令牌作为认证信息）

## 检查SSH Agent服务状态 {id="SSH_1"}
`win+R` 打开运行  
输入： `services.msc`  
找到：OpenSSH Authentication Agent  
设置为自动启动  
---（如果还没有用的话，在git bash页面，输入下面命令）---  
首先执行 exec ssh-agent bash 来启动一个新的bash实例，其中SSH代理被启动。  
然后执行 eval ssh-agent -s 来设置环境变量。  
最后执行 ssh-add "D:\blog\.ssh\id_rsa" 来添加你的私钥  

## 443端口
如果在配置了ssh-agent还有密钥(令牌)，还是无法使用  
`ssh -T git@github.com`成功连接github,  
可以试试`ssh -T -p 443 git@ssh.github.com`如果成功，说明主要问题出现在22端口无法访问，  
在这个路径：`C:\Users\[用户名]\.ssh`找到文件`config`,编辑加入下面这段：  
```Bash
Host github.com
  HostName ssh.github.com
  User git
  Port 443
```
