# 创建Private Key Store

Private Key Store可以帮助您管理和使用硬件安全模块HSM（Hardware Security Module）中的密钥。本文为您介绍如何创建Private Key Store。

Private Key Store需要关联同一阿里云账号下加密服务（Alibaba Cloud Data Encryption Service）的HSM集群。请确保加密服务已完成以下设置：

1.  已经创建HSM集群。
2.  集群中已经添加HSM实例。为了HSM集群高可用，建议您添加两个及以上HSM实例。
3.  已经完成集群的初始化。当前集群状态为**已初始化**。初始化时您设置的**ClusterOwnerCertificate**将作为KMS访问HSM的安全域证书。
4.  创建一个用户名为`kmsuser`的加密用户，并为`kmsuser`设置口令。KMS将使用该用户身份访问您的HSM集群，进行密钥创建和密码运算。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择Private Key Store所在的地域。

    支持Private Key Store的地域，请参见[支持的地域](/intl.zh-CN/密钥服务/Private Key Store/Key Store概述.md)。

3.  在左侧导航栏，单击**KeyStores**。

4.  单击**创建KeyStore**。

5.  在弹出的创建KeyStore对话框，配置以下参数。

    -   **名称**：输入Private Key Store名称。
    -   **HSM集群**：选择加密服务（Alibaba Cloud Data Encryption Service）的HSM集群。
    -   **描述**：输入Private Key Store描述信息。
    -   **口令**：输入加密服务（Alibaba Cloud Data Encryption Service）中用户`kmsuser`的口令。
    -   **安全域证书**：输入或上传加密服务（Alibaba Cloud Data Encryption Service）的HSM集群对应的安全域证书。
6.  单击**确定**。


Private Key Store创建成功后，默认处于**连接断开**状态。如果需要在Private Key Store中创建用户主密钥，您需要先连接Private Key Store。具体操作，请参见：

1.  [连接Private Key Store](/intl.zh-CN/密钥服务/Private Key Store/连接或断开Private Key Store.md)
2.  [创建密钥](/intl.zh-CN/快速入门/管理和使用密钥/创建密钥.md)

