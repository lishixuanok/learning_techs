# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | Spark安装指南 |

## Spark2.2在CentOS7上安装

### 安装相关环境

1. 安装Java

> sudo yum install java

> java -version

2. 安装Scala

> 下载Scala 2.11.x: http://www.scala-lang.org/files/archive/

解压archive

> tar -xvf your_scala_file.tgz

移动解压文件

> sudo mv your_scala_file /usr/local

> sudo ln -s /usr/local/you_scala_file /usr/local/scala

将可执行二进制文件导入到环境变量中

> export PATH=$PATH:/usr/local/scala/bin

检查Scala版本

> scala -version

返回版本信息则成功

> Scala code runner version 2.11.11 -- Copyright 2002-2017, LAMP/EPFL

3. 安装Spark

> tar xvf your_Spark_file.tgz

> sudo mv your_Spark_file /usr/local

> export PATH=$PATH:/usr/local/spark/bin

检查Spark安装成功

> spark_shell

返回scala则成功

> scala> 

## Spark1.6在Docker上安装

拉取镜像

> docker pull sequenceiq/spark:1.6.0

运行镜像

> docker run -it -p 8088:8088 -p 8042:8042 -p 4040:4040 -h sandbox sequenceiq/spark:1.6.0 bash

检查成功

> /usr/local/spark/bin/spark_shell

返回scala则成功

> scala>


