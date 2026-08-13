# [huggingface][download]下载huggingface模型仓库linux方法

```Bash
# 安装命令
pip install -U huggingface_hub hf-transfer -i https://pypi.tuna.tsinghua.edu.cn/simple

# 临时更改镜像源
export HF_ENDPOINT=https://hf-mirror.com

# 暂时不知道有什么作用
export HF_HUB_ENABLE_HF_TRANSFER=1 

# 下载命令[zai-org/GLM-4.7-Flash]、[ ./GLM-4.7-Flash]这两个根据实际情况替换，这是断点续传的命令，下载中止了，后面也可以用
huggingface-cli download zai-org/GLM-4.7-Flash --local-dir ./GLM-4.7-Flash --local-dir-use-symlinks False --resume-download
```
