# [faiss]向量数据库入门

> **作用**：可以结合其它模型，把各种数据转化为向量，作为单机运行的小批量暂时保存的向量数据库，用于进行向量之间的相似度检索。
> 但无法根据检索的向量还原成本来的数据，有该需求需要额外保存原始文字or图片的索引。
> 如果想要持久化保存知识库，推荐部署milvus。

## 1.安装
只需要在python环境下，安装faiss模块即可，命令如下：
```Bash
pip install faiss-gpu
#pip install faiss-cpu #如果是没有gpu的设备

pip install numpy==1.24.4 #注意，numpy必须要是1.x版本的，2.0以上版本会报错
```

## 2.快速上手

### 2.1.查看faiss是否检索到了本机的gpu
```Python
import faiss
print(faiss.get_num_gpus()) #faiss.get_num_gpus()会返回faiss查询到的gpu个数
```

### 2.2.创建faiss向量数据库，增删改查

创建faiss向量数据库需要指定一个参数，即每个向量的长度。
```python
import faiss
# 指定向量长度
d = 512 
# 将向量的长度传递给 faiss.IndexFlatL2 函数，建立一个空的索引容器
index = faiss.IndexFlatL2(d) 
```
<br></br><br></br>


数据库新增向量
```Python
import random
import numpy as np
for i in range(10):
    # 创建长度512的向量
    vec = np.array([[random.uniform(-10,10) for _i in range(512)]],dtype=np.float32) 
    # 装入数据库
    index.add(vec) 
    
# 获取向量数量
index.ntotal 

"""输出
10
"""
```
*(需要注意：faiss数据库存入的向量需要是numpy格式，且shape需要是2，如vec.shape = (1,512))*
<br></br><br></br>


★数据库查询向量（faiss的核心功能，根据空间距离，查询最接近的向量）
```python
# 创建一个查询向量
query = np.random.random((1, d)).astype('float32') 

#进行 k-NN查询
k = 3 
# 返回最近的k个向量
distances,labels = index.search(query,k)
print("Distances:", distances) # distances是检索最近k个向量的距离
print("Labels:", labels) # labels是检索最近k个向量的标签


"""输出
Distances: [[17114.654 17249.977 17404.52 ]]
Labels: [[2 4 3]]
"""
```
<br></br><br></br>

数据库删除向量
```python
print("当前向量个数："+index.ntotal)
idx_to_rm= np.array([1,2]) #要删除的下标
#使用remove_ids()函数删除
index.remove_ids(idx_to_rm) 
print("删除后向量个数："+index.ntotal)

"""输出
当前向量个数：10
删除后向量个数：8
"""
```
*(注意：remove_ids()参数为numpy数组，表示要删除的向量索引)*
<br></br><br></br>

数据库改动向量
```python
# 略（没有直接的方法，一般通过先删除向量，再新增向量，来做到修改的目的）
```

## 3.faiss数据的保存与加载
```Python
# faiss索引保存
def faiss_index_save(faiss_index, save_file_location):
    faiss.write_index(faiss_index, save_file_location)
# faiss索引加载
def faiss_index_load(faiss_index_save_file_location):
    index = faiss.read_index(faiss_index_save_file_location)
    return index
```

## 4.faiss的其它距离计算算法
在 FAISS 中，切换不同的距离计算算法主要通过选择不同的索引类型来实现。以下是一些常见的索引类型及其对应的距离计算算法：
- IndexFlatL2：计算 L2 距离（欧几里得距离）。
- IndexFlatIP：计算内积（点积）。
- IndexIVFFlat：基于倒排文件（IVF）的索引，支持 L2 距离和内积。
- IndexIVFPQ：基于倒排文件和积量化的索引，支持 L2 距离和内积。
```Python
# 1.创建 L2 距离索引
index = faiss.IndexFlatL2(d)

# 2.创建内积索引
index = faiss.IndexFlatIP(d)

# 3.余弦相似度(通过先对向量进行归一化，再进行内积计算余弦相似度)
# 略

# 4.倒排文件（IVF）索引：L2 距离
# 创建 IVF 索引
quantizer = faiss.IndexFlatL2(d)  # 量化器
index = faiss.IndexIVFFlat(quantizer, d, 20, faiss.METRIC_L2)
# 训练索引
index.train(data)
# 添加数据集到索引
index.add(data)

# 5.倒排文件（IVF）索引：内积
# 创建 IVF 索引
quantizer = faiss.IndexFlatIP(d)  # 量化器
index = faiss.IndexIVFFlat(quantizer, d, 20, faiss.METRIC_INNER_PRODUCT)
# 训练索引
index.train(data)
# 添加数据集到索引
index.add(data)
```




