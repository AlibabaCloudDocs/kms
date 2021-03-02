# 连接或断开Private Key Store

本文为您介绍如何连接或断开Private Key Store。

## 连接Private Key Store

Private Key Store创建成功后，如果需要在Private Key Store中创建用户主密钥，您需要先连接Private Key Store。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择Private Key Store所在的地域。

    支持Private Key Store的地域，请参见[支持的地域](/cn.zh-CN/密钥服务/Key Store/Key Store概述.md)。

3.  在左侧导航栏，单击**KeyStores**。

4.  在Private Key Store右侧**操作**列，单击**连接**。

    连接成功后Private Key Store状态变为**已连接**，此时您可以在Private Key Store中创建用户主密钥。具体操作，请参见[创建密钥](/cn.zh-CN/快速入门/管理和使用密钥/创建密钥.md)。


## 断开Private Key Store

如果需要删除Private Key Store，您需要先断开Private Key Store连接。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择Private Key Store所在的地域。

    支持Private Key Store的地域，请参见[支持的地域](/cn.zh-CN/密钥服务/Key Store/Key Store概述.md)。

3.  在左侧导航栏，单击**Key Store**。

4.  在Private Key Store右侧**操作**列，单击**断开**。

5.  在弹出的断开KeyStore对话框，单击**确定**。

    断开成功后Key Store状态变为**连接断开**，此时您不能在Private Key Store中创建和使用您的用户主密钥，但是可以删除用户主密钥。


