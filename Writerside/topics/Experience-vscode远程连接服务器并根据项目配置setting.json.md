# [Experience]vscode远程连接服务器并根据项目配置setting.json

## vscode连接好远程服务器，打开项目文件，按下快捷键：`Ctrl+Shift+P`
![image_4.png](image_4.png)

## 搜索setting.json
这边可以看到不同范围的setting.json，这边以文件夹（项目）为单位，即在打开的文件夹内创建setting.json，选择第一个“打开工作区设置（JSON）”。

![image_5.png](image_5.png)

然后你的文件目录下，就会多一个.vscode/setting.json的文件，相关配置可以写在那里面。

![image_6.png](image_6.png)

## 样例1：vscode里面的关键词，没办法通过Ctrl+右键跳转
分析：大概率是vscode没有索引到python所处的环境，可以在setting.json中敲入下面代码;
```bash
{
	// 需要被诊断的文件的路径信息
	"python.analysis.include": [
		"python环境路径1",
        "python环境路径2",
        ...
	],
}
```
如下图，我把python环境的路径和项目路径，都放入了"python.analysis.include"里面，这样vscode就可以跳转两个路径下的定义好的函数了。

![image_7.png](image_7.png)

* 其他打开setting.json的方法，以及setting.json可以配置哪些功能，可以参考博客：[如何打开并且配置vscode的setting.json文件](https://blog.csdn.net/daishu_shu/article/details/131439706) *
