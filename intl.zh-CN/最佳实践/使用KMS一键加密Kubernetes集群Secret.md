# 使用KMS一键加密Kubernetes集群Secret

阿里云容器服务Kubernetes版（简称ACK）通过您指定的KMS主密钥，对Kubernetes集群Secret进行落盘加密，您只需一键配置即可实现对Kubernetes集群的安全保护。

## 使用场景

Kubernetes拥有强大的运维编排管理能力，依赖大量的跨产品、跨服务、跨模块调用所必须使用的机密信息，例如：密码、证书、凭据、访问密钥等。Kubernetes集群使用Secret模型存储和管理集群系统和集群中业务应用的敏感信息，并且通过内部的etcd集群进行保存，同时在etcd集群的副本中进行分布式复制存储。

例如：部署一个没有任何业务负载的Kubernetes集群，初始情况下有大约50个Secret。其中任何一个Secret的泄露，都可能对Kubernetes集群、业务系统，甚至是企业的运行产生不可估量的损失。因此您在享受Kubernetes为您带来的便利时，也需要对Kubernetes集群中托管的大量凭据进行必要的保护，防止来自各方面的安全威胁。

## 加密机制

在ACK Pro托管集群中，您可以使用在KMS中创建的用户主密钥（CMK）加密Kubernetes Secret，加密过程基于Kubernetes提供的[KMS Encryption Provider机制](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/)，使用信封加密的方式对存储在etcd中的Kubernetes Secret密钥进行自动加密和解密。关于信封加密的详情，请参见[什么是信封加密？](/intl.zh-CN/常见问题/什么是信封加密？.md)。Kubernetes Secret密钥加密和解密的过程如下：

-   当一个业务密钥需要通过Kubernetes Secret API存储时，数据会首先被API Server生成的一个随机的数据密钥加密，然后该数据密钥会被指定的KMS用户主密钥（CMK）加密为一个密文密钥存储在etcd中。
-   解密Kubernetes Secret密钥时，系统会首先调用KMS的解密API进行密文密钥的解密，然后使用解密后的明文密钥对Secret数据解密并最终返回给用户。

## 前提条件

-   您需要为使用Kubernetes的账号授予AliyunCSManagedSecurityRole角色的权限。如果您使用的账号未授权，在创建Pro集群或修改已有Pro集群过程中开启Secret落盘加密时，系统会提示您进行安全系统角色授权。
-   如果您使用RAM用户登录，请确保RAM用户具备AliyunKMSCryptoAdminAccess权限。具体操作，请参见[为RAM用户授权](/intl.zh-CN/用户管理/为RAM用户授权.md)。
-   请确保您已在KMS控制台创建用户主密钥（CMK）。具体操作，请参见[创建密钥](/intl.zh-CN/快速入门/管理和使用密钥/创建密钥.md)。

    **说明：** 仅支持Aliyun\_AES\_256类型的用户主密钥（CMK）。


## 在新创建的ACK Pro集群中开启Secret落盘加密

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏，单击**集群**。

3.  单击页面右上角的**创建集群**，在弹出的选择集群模板对话框，选择Pro版集群，并单击**创建**。

4.  在**ACK托管版**页签找到**Secret落盘加密**，选中**选择KMS密钥**，在下拉列表中选择KMS密钥ID。

    ![加密](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0816119951/p144069.png)

5.  根据控制台提示完成其他参数设置。具体操作，请参见[创建Kubernetes Pro版集群](/intl.zh-CN/Kubernetes集群用户指南/ACK Pro集群/创建Kubernetes Pro版集群.md)。


## 在已创建的ACK Pro集群中开启Secret落盘加密

1.  登录[容器服务管理控制台](https://cs.console.aliyun.com)。

2.  在左侧导航栏，单击**集群**。

3.  在集群列表页面单击目标Pro集群名称。

4.  在集群详情页面单击**基本信息**页签，在**基本信息**区域中打开**Secret落盘加密**开关。

    当集群状态由**更新中**变为**运行中**时，说明该集群Secret落盘加密的特性已变更完成。


## 执行结果

如果您在操作审计控制台的**详细事件查询**页面获取到使用AliyunCSManagedSecurityRole系统角色的加密和解密操作事件，则说明该集群已成功开启Secret落盘加密特性，此时您可以通过操作审计控制台查看对KMS的所有调用记录。

