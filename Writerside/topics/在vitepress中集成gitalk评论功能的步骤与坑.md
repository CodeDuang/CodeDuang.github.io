# 在vitepress中集成gitalk评论功能的步骤与坑

## 概要
原理：评论需要登陆github账户，每次评论相当于在github仓库中发issues，利用github仓库的issues来存放和管理每个用户的评论，然后gitalk调用api来显示到页面上，以达到评论和显示他人评论的目的。
总体步骤：首先需要完成github上OAuth应用的注册，然后下载gitalk组件，最后就是在vitepress的md页面中用代码显示gitalk评论栏与实现功能。
主要参考文档与博客：  
1.[官方文档](https://github.com/gitalk/gitalk/blob/master/readme-cn.md)  
2.[因为VitePress没有像VuePress那样的可以直接安装配置的评论插件，所以就需要自己动手，这里使用gitalk作为插件使用](https://younglina.top/write/docs/vitepress-gitalk.html)  
## 第一步，github注册OAuth应用
登录github，点击右上角用户头像，下拉菜单中点击“Settings”跳转页面

![image_36.png](image_36.png){border-effect=line}

在左侧的的菜单栏中，点击最下面的“Developer settings”进入新页面

![image_37.png](image_37.png){border-effect=line}

选择“OAuth Apps”然后点击“New OAuth App”新键app

![image_38.png](image_38.png){border-effect=line}

图片参考了（用鼠标写字好慢）：https://younglina.top/write/docs/vitepress-gitalk.html

![image_39.png](image_39.png){border-effect=line}

（说明一下，图中的回跳地址的意思是用户登录了github账户之后，跳转的地址，建议填写要放置评论的页面链接。）

创建好后会给你一个`Client ID`和`Client Secret`，后者不可找回，一定要复制保存好，后面用的上。

## 第二步，下载gitalk组件（windows环境）
安装了vue的话，直接用下面的命令即可
```
npm i --save gitalk
```
## 第三步，vitepress对应md页面添加相关代码
```js
<script setup>
import "gitalk/dist/gitalk.css";
import Gitalk from "gitalk";
import { onMounted } from 'vue';
onMounted(() => {
  if(typeof window !==undefined){
    var s_div = document.createElement('div');   // 创建节点
    s_div.setAttribute("id", "gitalk-page-container");   // 设置id
    document.querySelector('.content-container').appendChild(s_div);   // querySelector的节点可自己根据自己想加载的地方设置
    var gitalk = new Gitalk({  //（上面的都不要改，从这里开始填写信息）
        clientID: '8d8e96********797026d3',          // 填写之前创建OAuth App保存的clientID
        clientSecret: '235****234jkas12',  // 填写之前创建OAuth App保存的clientSecret
        repo: 'blogtalk',          // 填写你用于存放评论的仓库名，注意需要仓库打开了issues功能（一般默认打开）
        owner: 'CodeDuang',   // 填写你的github用户名
        admin: ['CodeDuang'], // 填写github管理者列表
        id: decodeURI(location.pathname),      // 不变，Ensure uniqueness and length less than 50
        distractionFreeMode: false  // 不变，Facebook-like distraction free mode
    })
    gitalk.render('gitalk-page-container')
  }
})
</script>
<div id="gitalk"></div>
```


填写情况如图所示（我想在contact.md页面加入评论功能，则在该md文件中加入相关代码）

![image_40.png](image_40.png){border-effect=line}

### 代码解释
虽然是md文件，但在上面代码中，用
```js
<script setup>
	
</script>
```
框住了用js代码进行gitalk配置的部分，这在vitepress中是允许的。

---
代码中的下面两段，是引入下载的gitalk组件，方便之后直接创建Gitalk对象
```js
import "gitalk/dist/gitalk.css";
import Gitalk from "gitalk";
```
---
下面的代码创建了Gitalk对象，用于和github上面你创建的OAuth App进行联系，同时指定了评论存放的仓库名。

```js
var gitalk = new Gitalk({  //（上面的都不要改，从这里开始填写信息）
        clientID: '8d8e96********797026d3',          // 填写之前创建OAuth App保存的clientID
        clientSecret: '235****234jkas12',  // 填写之前创建OAuth App保存的clientSecret
        repo: 'blogtalk',          // 填写你用于存放评论的仓库名，注意需要仓库打开了issues功能（一般默认打开）
        owner: 'CodeDuang',   // 填写你的github用户名
        admin: ['CodeDuang'], // 填写github管理者列表
        id: decodeURI(location.pathname),      // 不变，Ensure uniqueness and length less than 50
        distractionFreeMode: false  // 不变，Facebook-like distraction free mode
    })
gitalk.render('gitalk-page-container')
```
---

对gitalk评论模块的展示，可以直接使用html语句
```html
<div id="gitalk"></div>
```
因为vitepress也允许在md文件中直接使用html的一些标签，比如\<div>

---

注意：大部分教程并没有下面这一段代码
```md
import { onMounted } from 'vue';
onMounted(() => {
  if(typeof window !==undefined){
    var s_div = document.createElement('div');   // 创建节点
    s_div.setAttribute("id", "gitalk-page-container");   // 设置id
    document.querySelector('.content-container').appendChild(s_div);   // querySelector的节点可自己根据自己想加载的地方设置
```
因为vitepress无法识别window字段，但gitalk需要window.document字段加载节点，所以需要下面代码对window字段进行补充。（不用做额外的操作，只是摘出上面的代码进行解释）

## 预览

![image_41.png](image_41.png){border-effect=line}

如果评论模块显示404，说明没有连接到对应仓库issues，可以检查一下仓库名是否正确（只用仓库名，不是网址），以及你的用户名是否填正确（github用户除了用户名还有个昵称，注意区分用户名和昵称！！！），最后就是检查你的仓库打开issues没有。（总之，还是建议新建一个仓库用来专门存放评论内容）

如果干脆就没显示评论模块，可能是代码上有什么问题，按F12查看网页加载时的报错，以定位出问题的地方。
## 小结

花了蛮多时间的，完全没学过js和vue，脑袋都扣烂了，主要就是怎么在md文件中使用js语法，以及vitepress里面对window字段的报错，理论上我的两篇参考文档就可以解决大部分问题了。
