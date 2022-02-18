---
title: ClickHouse初始
categories:
 - 数据库
tags:
---

`ClickHouse`是一个用于联机分析 (`OLAP`) 的列式数据库管理系统 (`DBMS`). 由俄罗斯搜索引擎巨头 Yandex 开源. 主要用于数据分析领域, 目前国内社区火热, 各个大厂纷纷跟进大规模用于 OLAP 领域。

## ClickHouse简介

`ClickHouse`是一个用于联机分析 (`OLAP`) 的列式数据库管理系统 (`DBMS`). 由俄罗斯搜索引擎巨头 Yandex 开源. 主要用于数据分析领域, 目前国内社区火热, 各个大厂纷纷跟进大规模用于 OLAP 领域。

ClickHouse官网上面介绍的特性：

- **快速**：ClickHouse会充分利用所有可用的硬件，以尽可能快地处理每个查询。单个查询的峰值处理性能超过每秒 2 TB（解压缩后，仅使用的列）。在分布式设置中，读取是在健康副本之间自动平衡的，以避免增加延迟。
- **容错**：ClickHouse支持多主机异步复制，并且可以跨多个数据中心进行部署。所有节点都相等，这可以避免出现单点故障。单个节点或整个数据中心的停机时间不会影响系统的读写可用性。
- **可伸缩**：ClickHouse可以在垂直和水平方向上很好地缩放。 ClickHouse易于调整以在具有数百或数千个节点的群集上或在单个服务器上，甚至在小型虚拟机上执行。当前，每个单节点安装的数据量超过数万亿行或数百兆兆字节。
- **易用**：ClickHouse简单易用，开箱即用。它简化了所有数据处理：将所有结构化数据吸收到系统中，并且立即可用于构建报告。 SQL允许表达期望的结果，而无需涉及某些DBMS中可以找到的任何自定义非标准API。

## ClickHouse安装教程

ClickHouse 可以在任何具有 x86_64 ，AArch64 或 PowerPC64LE CPU 架构的 Linux ，FreeBSD 或 Mac OS X 上运行。貌似不能在 Windows 系统下安装，不过 ClickHouse 同样支持 Docker 部署，Windows 系统可以在 Docker 下安装 ClickHouse 。

下面以CentOS系统为例，以rpm方式来安装ClickHouse。

```shell
# 查看系统版本
[root@master ~]# more /etc/redhat-release 
CentOS Linux release 7.9.2009 (Core)

# 检测当前CPU是否支持SSE 4.2
[root@master ~]# grep -q sse4_2 /proc/cpuinfo && echo "SSE 4.2 supported" || echo "SSE 4.2 not supported"
SSE 4.2 supported

# 添加官方存储库
sudo yum install yum-utils
sudo rpm --import https://repo.clickhouse.tech/CLICKHOUSE-KEY.GPG
sudo yum-config-manager --add-repo https://repo.clickhouse.tech/rpm/stable/x86_64

# 安装clickhouse
sudo yum install clickhouse-server clickhouse-client

# 启动clickhouse
sudo /etc/init.d/clickhouse-server start

# 进入clickhouse客户端
[root@master ~]# clickhouse-client
ClickHouse client version 21.12.3.32 (official build).
Connecting to localhost:9000 as user default.
Connected to ClickHouse server version 21.12.3 revision 54452.

# 开启远程连接


```

