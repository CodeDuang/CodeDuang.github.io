# 如何设置命令行or终端代理

参考博客：

[windows终端命令行下使用网络代理](https://www.cnblogs.com/macrored/p/12190799.html)

*这边演示的是windows系统*

## 找到端口信息

![image_8.png](image_8.png)

我这边显示的是走10809端口

## 打开cmd窗口，敲如下命令
```bash
set HTTP_PROXY=http://127.0.0.1:10809
set HTTPS_PROXY=http://127.0.0.1:10809
```

## 测试
```bash
curl -v www.google.com
```

命令运行前（超时）：↓

![image_9.png](image_9.png)

命令运行后：↓

![image_10.png](image_10.png)

