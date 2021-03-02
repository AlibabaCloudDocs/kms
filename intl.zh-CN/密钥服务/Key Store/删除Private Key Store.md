# 删除Private Key Store

本文为您介绍如何删除Private Key Store。删除后您无法通过KMS管理和使用Private Key Store中的密钥。如果您的密钥已经用于线上应用程序，请谨慎操作，避免影响线上业务。

删除Private Key Store前，请确保您已经完成以下操作：

1.  计划删除Private Key Store中的所有用户主密钥。具体操作，请参见[计划删除密钥](/intl.zh-CN/密钥服务/管理密钥/计划删除密钥.md)。
2.  用户主密钥删除完成后，断开Private Key Store连接。具体操作，请参见[断开Private Key Store](/intl.zh-CN/密钥服务/Key Store/连接或断开Private Key Store.md)。

**说明：** 如果在用户主密钥计划删除前断开Private Key Store连接，密钥管理服务将删除存储在Private Key Store中密钥元数据（非敏感信息），但是无法删除关联加密服务HSM中的密钥。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择Private Key Store所在的地域。

    支持Private Key Store的地域，请参见[支持的地域](/intl.zh-CN/密钥服务/Key Store/Key Store概述.md)。

3.  在左侧导航栏，单击**KeyStores**。

4.  在Private Key Store右侧**操作**列，单击**删除**。

5.  在弹出的删除KeyStore对话框，单击**确定**。


