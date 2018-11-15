---
title: zookeeper伪分布式搭建
date: 2018-11-15
description: 
categories:
 - 分布式
 - zookeeper
tags:
 - 分布式
 - zookeeper
---

> zookeeper伪分布式搭建

#### 一、描述

伪分布式集群就是在一台机器部署多个zk应用，部署之前服务器需要有jdk环境 java -version可以显示相关java信息才可以进行zookeeper搭建

#### 二、步骤

- 第一步下载好zookeeper-3.4.9.tar.gz
- 然后解压tar -zxvf zookeeper-3.4.9.tar.gz
- 进入zk中的conf目录下输入

```
cp zoo-sample.cfg zoo1.cfg  cp zoo-sample.cfg zoo2.cfg、cp zoo-sample.cfg zoo3.cfg  
```

- 分别对zoo1、2、3文件进行编辑

```
# The number of milliseconds of each tick
tickTime=2000
# The number of ticks that the initial 
# synchronization phase can take
initLimit=10
# The number of ticks that can pass between 
# sending a request and getting an acknowledgement
syncLimit=5
# the directory where the snapshot is stored.
# do not use /tmp for storage, /tmp here is just 
# example sakes.
#不同zoo.cfg修改自己的目录
dataDir=/apps/servers/data/d_1
dataLogDir=/apps/servers/logs/logs_1
# the port at which the clients will connect
#不同zoo.cfg修改自己的端口号
clientPort=2181 
# the maximum number of client connections.
# increase this if you need to handle more clients
#maxClientCnxns=60
#
# Be sure to read the maintenance section of the 
# administrator guide before turning on autopurge.
#
# http://zookeeper.apache.org/doc/current/zookeeperAdmin.html#sc_maintenance
#
# The number of snapshots to retain in dataDir
#autopurge.snapRetainCount=3
# Purge task interval in hours
# Set to "0" to disable auto purge feature
#autopurge.purgeInterval=1
server.1=localhost:2187:2887 
server.2=localhost:2188:2888
server.3=localhost:2189:2889

```

- 修改之后分别创建data目录和日志目录,并写入myid

```
mkdir /apps/servers/data/d_1
Mkdir /apps/servers/data/d_1
mkdir /apps/servers/data/d_1

mkdir /apps/servers/logs/logs_1
mkdir /apps/servers/logs/logs_1
mkdir /apps/servers/logs/logs_1

echo "1" > /apps/servers/data/d_1/myid
echo "2" >/apps/servers/data/d_2/myid
echo "3" >/apps/servers/data/d_3/myid

```

- 进入bin目录下输入命令 分别进行启动

```
zkServer.sh start ../conf/zoo1.cfg
zkServer.sh start ../conf/zoo2.cfg
zkServer.sh start ../conf/zoo3.cfg

```



- 通过命令检测是否成功：

```
zkCli.sh -server localhost:2181,localhost:2182,localhost:2183
```


- 至此Zookeeper搭建结束，下面开始启动Zookeeper,分别启动：如果你不想切换到Zookeeper目录启动，可以配置环境变量：

```
vim /etc/profile (修改文件)

export ZOOKEEPER_HOME=/usr/local/zookeeper-3.4.13
export PATH=${ZOOKEEPER_HOME}/bin:$PATH

重新编译文件：
source /etc/profile 

```



*标记：人生在世，无非是让别人笑笑，偶尔，也笑笑别人。 - 郭德纲*







