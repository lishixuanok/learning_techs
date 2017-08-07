# Basic

|   layout   |    title   |
|:----------:|:----------:|
|   post     | Spark安装指南 |

## Spark2.2在CentOS7上安装

### 安装相关环境

1. 安装Java

```shell
$ sudo yum install java
```

```shell
$ java -version
```

2. 安装Scala

下载Scala 2.11.x

```shell
$ wget http://www.scala-lang.org/files/archive/
```

解压archive

```shell
$ tar -xvf your_scala_file.tgz
```

移动解压文件

```shell
$ sudo mv your_scala_file /usr/local
$ sudo ln -s /usr/local/you_scala_file /usr/local/scala
```

将可执行二进制文件导入到环境变量中

```shell
$ export PATH=$PATH:/usr/local/scala/bin
```

检查Scala版本

```shell
$ scala -version
```

返回版本信息则成功


```shell
$ Scala code runner version 2.11.11 -- Copyright 2002-2017, LAMP/EPFL
```

3. 安装Maven

若使用Scala/Java, 可使用Maven作构建


```shell
$ wget http://www-eu.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
```

```shell
$ export PATH=/usr/local/apache-maven-3.3.9/bin:$PATH
```

JAVA_HOME配置

```shell
$ export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:/bin/java::")
```

检查配置成功

```shell
$ mvn --version
```

### 安装Spark

```shell
$ tar xvf your_Spark_file.tgz
```

```shell
$ sudo mv your_Spark_file /usr/local
$ export PATH=$PATH:/usr/local/your_spark_file/bin
```

检查Spark安装成功

```shell
$ spark-shell
```

返回scala则成功

```shell
$ scala> 
```

## Spark1.6在Docker上安装

拉取镜像

```shell
$ docker pull sequenceiq/spark:1.6.0
```

运行镜像

```shell
$ docker run -it -p 8088:8088 -p 8042:8042 -p 4040:4040 -h sandbox sequenceiq/spark:1.6.0 bash
```

检查成功

```shell
$ /usr/local/spark/bin/spark_shell
```

返回scala则成功

```shell
$ scala>
```

### 持久化添加linux环境变量

修改用户路径下的.bash_profile

```shell
vi /home/your_user/.bash_profile
```

修改环境变量
```shell
PATH=$PATH:$HOME/.local/bin:$HOME/bin:/usr/local/scala/bin:/usr/local/apache-maven-3.3.9/bin:/usr/local/spark-2.2.0-bin-hadoop2.7/bin/

export PATH

export JAVA_HOME=$(readlink -f /usr/bin/java | sed "s:/bin/java::")

```

修改完重启机器即可

```shell
reboot
```
