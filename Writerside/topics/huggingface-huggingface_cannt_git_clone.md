# [huggingface]huggingface cannt git clone

## 问题描述：
在ubuntu系统上，使用如下命令，克隆仓库，报无法访问错误：
```bash
git clone https://huggingface.co/distilbert/distilroberta-base
```
![image.png](image.png)

## 通用解决方案：
把下面部分更换：

```bash
https://huggingface.co/....
↓
https://hf-mirror.com/....
```
![image_2.png](image_2.png)

*（模型大，会下一会，可以通过查看网络带宽情况判断是否在下载）*

## 其它问题：
发现模型并没有被下载下来（整个文件夹不应该只有5.3M）：
![image_3.png](image_3.png)

原因：当你使用 git clone 命令来克隆一个仓库时，如果仓库中包含了大文件，比如机器学习模型的权重文件，通常会使用 Git Large File Storage (LFS) 来处理这些大文件。Git LFS 是一个 Git 扩展，用于更有效地处理大型二进制文件。
命令更改（git-lfs工具自行下载）：
```bash
git clone ...
↓
git lfs clone ...
```
*（实际上，git-lfs工具下好了，使用git clone会自动调用git lfs clone）*

*博客从我自己的csdn上搬运来的，图片水印什么的懒得改了*