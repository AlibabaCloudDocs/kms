# 动态RAM凭据概述

RAM凭据是指RAM用户的访问密钥（AccessKey），包括AccessKey ID和AccessKey Secret，用于RAM用户在调用阿里云API时完成身份验证。凭据管家可以对托管的RAM凭据进行全自动的定期轮换，将静态的RAM凭据动态化，从而降低RAM凭据泄漏的风险。除定期轮转外，凭据管家还支持立即轮转，在RAM凭据泄漏情况下快速更换AccessKey。

## 使用动态RAM凭据

使用动态RAM凭据，您无需在应用程序中配置AccessKey。管理员在凭据管家创建动态RAM凭据，设置自动轮转周期之后，应用程序调用[GetSecretValue](/intl.zh-CN/API参考/凭据/GetSecretValue.md)接口获取有效的AccessKey，用于调用阿里云API。

RAM凭据轮转成功后，凭据关联的RAM用户的AccessKey将同步发生更新。请您不要删除凭据关联的RAM用户，避免凭据轮转失败。

![动态RAM凭据架构图](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6346619161/p267587.png)

动态RAM凭据操作流程如下：

1.  [授予凭据管家管理RAM用户AccessKey的权限]()。
2.  [创建动态RAM凭据]()。
3.  [应用程序接入凭据管家](/intl.zh-CN/凭据管家/应用程序接入凭据管家.md)。
4.  使用RAM凭据访问阿里云服务。

## 使用限制

当前凭据管家只支持托管RAM用户的AccessKey，不支持托管阿里云账号的AccessKey。

