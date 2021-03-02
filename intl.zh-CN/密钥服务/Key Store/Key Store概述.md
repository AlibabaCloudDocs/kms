# Key Store概述

Key Store是KMS中的密钥安全域，包含了您创建的密钥元数据（非敏感信息），以及用于密钥存储和密码计算的资源设施。不同Key Store中的密钥被安全地隔离起来，这不仅是密钥存储、密码计算所使用资源的隔离，也是密码学上的隔离。

## 支持的地域

支持Key Store的地域为：新加坡。

## 产品优势

KMS提供默认的Key Store，同时允许您定义Private Key Store，方便您管理和使用同一阿里云账号下硬件安全模块HSM（Hardware Security Module）中的密钥。使用Private Key Store具有以下优势：

-   相比默认的Key Store，Private Key Store使用独享的HSM资源，实现资源隔离和密码学隔离，获得更高的安全性。
-   降低使用HSM的复杂度，为您的HSM提供稳定、易用的上层密钥管理和密码计算服务。
-   将您的HSM与云服务无缝集成，为云服务加密提供更高的安全性和可控制性。更多信息，请参见[支持服务端集成加密的云服务](/intl.zh-CN/云产品与KMS的集成/支持服务端集成加密的云服务.md)。

## 产品架构

Private Key Store和加密服务（Alibaba Cloud Data Encryption Service）中的HSM集群相关联。Private Key Store中用户主密钥的存储和使用都不会离开HSM集群的边界，为您的密钥管理和使用提供更高的安全性。

![架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5961334161/p243332.png)

## 使用Private Key Store

当您需要使用Private Key Store管理您的用户主密钥时，请进行以下操作：

1.  在[加密服务控制台](https://yundun.console.aliyun.com/?p=hsm)进行设置。
    1.  创建HSM集群。
    2.  在HSM集群中添加HSM实例。
    3.  初始化HSM集群。具体操作，请参见[Initialize HSM](/intl.zh-CN/Quick Start/Step 6: Initialize HSM.md)。
    4.  创建一个用户名为`kmsuser`的加密用户，并为`kmsuser`设置口令。具体操作，请参见[Create a crypto user](/intl.zh-CN/Quick Start/Step 8: Create a key.md)。
2.  在[密钥管理服务控制台](https://kms.console.aliyun.com)进行设置。
    1.  [创建Private Key Store]()。
    2.  [连接Private Key Store]()。
    3.  [创建密钥](/intl.zh-CN/快速入门/管理和使用密钥/创建密钥.md)。

密钥创建完成后，你可以通过API、CLI或SDK使用HSM中的密钥。

