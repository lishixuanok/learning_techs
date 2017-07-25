# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | Spark快速使用1 |

# Spark RDD

### 特点

1. RDD: Resilient Distributed Dataset.

> 弹性的分布式存储数据集。其中弹性是指某个节点挂掉，其他节点继续进行该节点的计算。

2. immutable.

> 无法在原有数据集上更改，只可读，在原有数据集计算生成新数据集。

### 数据流程

1. file text: 源数据

2. flat map: 拉平数据. [[1,2,3], [4,5,6]] --> [1,2,3,4,5,6]

3. map.

4. reduce. 

### 设计模式

1. transformations and actions.

2. lazy fashion-DAG(Directed Acyclic Graph) 

3. map(), filter(), flatmap()

### 注意的是

1. persis()持久化, 重复使用的RDD

2. 默认persist在内存，可配置到磁盘

3. collect()要保存到分布式存储系统中如HDFS

