# 动态RDS凭据概述

针对数据库的攻击是数据安全面临的主要威胁之一。针对阿里云关系型数据库RDS，凭据管家支持配置动态RDS凭据，对凭据进行全自动的定期轮换，降低业务数据面临的安全威胁。

## 产品架构

使用动态RDS凭据，应用程序将无需配置静态数据库账号口令。管理员在凭据管家创建全托管RDS凭据，设置自动轮转周期之后，应用程序调用[GetSecretValue](/intl.zh-CN/API参考/凭据/GetSecretValue.md)接口获取仅在下次轮转前有效的账号口令，用于访问RDS托管数据库。

RDS凭据轮转成功后，凭据关联的RDS实例的账号和口令将同步发生更新。请您不要删除凭据关联的RDS实例，避免凭据轮转失败。

![架构](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0473219061/p206606.png)

## 使用限制

动态RDS凭据支持特定的RDS数据库：RDS MySQL、RDS MariaDB TX、RDS SQL Server（2017集群版除外）和RDS PostgreSQL。

## 使用动态RDS凭据

1.  [t2005680.md\#section\_tgu\_kh8\_a02](/intl.zh-CN/凭据管家/动态RDS凭据/创建动态RDS凭据.md)
2.  [监控动态RDS凭据轮转](/intl.zh-CN/凭据管家/动态RDS凭据/监控动态RDS凭据轮转.md)
3.  [应用程序接入凭据管家](/intl.zh-CN/凭据管家/应用程序接入凭据管家.md)

