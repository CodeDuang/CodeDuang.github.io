# [Linux]查后台进程与nohup

省流：

```bash
#根据进程名查找UID
ps aux | grep [进程名]
#杀掉进程
kill -9 [进程UID]
```

实践：查杀nohup启动的后台进程
## 1.回顾你的nohup启动进程的命令（主要用来获取进程名，其他命令启动的进程同理，只需要知道进程的名字）
```bash
#这个指令的进程名为jupyter notebook（用jupyter也可以检索的到）
nohup jupyter notebook --allow-root > jupyter.log 2>&1 &

#这个指令的进程名为frps（用frp也可以检索到）
nohup ./frps -c frps.toml &
#（进程名可以少或者短，都可以检索到的）
```
## 2.查找进程UID（命令如下）

```bash
#模板
ps aux | grep [进程名]

#如果是frps进程，则可以是下面这样
ps aux | grep frps
```

![image_21.png](image_21.png)

如图为检索到的进程情况，第一行的就是我们启动的frps进程，该进程的UID为：`456486`
（第二行那个`grep --color=auto`不用管，无论你查找的进程名是什么都会出现这么一行的）
## 3.杀进程（命令如下）

```bash
#模板
kill -9 [进程UID] 

#如frps进程UID，就用下面代码杀掉
kill -9  456486
```

![image_22.png](image_22.png)

杀掉后，我们再用`ps aux | grep frps`查找一下情况，发现果然已经被杀掉了。