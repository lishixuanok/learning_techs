# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | Spark streaming use case |

## Spark Streaming应用场景

Spark Streaming 是能高可扩展、高吞吐、容错的Spark Core API的延伸，处理实时数据流。

数据输入：Kafka, Flume, Kinesis, or TCP sockets

数据处理：使用high level函数，如map, reduce, join and window，来进行复杂算法处理

数据输出：文件系统、数据库、live dashboard

Spark使用机器学习算法、图处理算法对数据进行处理。

## Spark Streaming工作流程

1. 数据流输入Spark Streamming，输出分块数据流

2. 分块数据流输入Spark Engine， 输出处理后的分块数据流


