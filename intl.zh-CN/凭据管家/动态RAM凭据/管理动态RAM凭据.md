# 管理动态RAM凭据

您可以创建动态RAM凭据，对RAM凭据进行全自动的定期轮换，从而降低RAM凭据泄露的安全风险。本文为您介绍如何通过KMS控制台创建、删除或还原动态RAM凭据。

-   阿里云账号和具有相关权限的RAM用户或RAM角色都可以管理动态RAM凭据。

    当RAM用户或RAM角色管理动态RAM凭据时，您需要将系统策略[AliyunKMSSecretAdminAccess](https://ram.console.aliyun.com/policies/AliyunKMSSecretAdminAccess/System/content)和[AliyunRAMFullAccess](https://ram.console.aliyun.com/policies/AliyunRAMFullAccess/System/content)授予该RAM用户或RAM角色。

-   管理动态RAM凭据前，您需要通过RAM服务角色授予凭据管家管理RAM用户AccessKey的权限。具体操作，请参见[授予凭据管家管理RAM用户AccessKey的权限](/intl.zh-CN/凭据管家/动态RAM凭据/授予凭据管家管理RAM用户AccessKey的权限.md)。
-   请为待托管RAM凭据的RAM用户创建AccessKey。具体操作，请参见[为RAM用户创建访问密钥](/intl.zh-CN/安全设置/访问密钥/为RAM用户创建访问密钥.md)。

## 创建动态RAM凭据

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择RAM凭据托管的地域。

3.  在左侧导航栏，单击**凭据**。

4.  单击**创建凭据**。

5.  在创建凭据对话框，配置以下参数，然后单击**下一步**。

    -   **选择凭据类型**：选择**托管RAM凭据**。
    -   **选择RAM用户**：选择您要托管凭据的RAM用户，所选RAM用户需要至少有一个AccessKey。
    -   **设置凭据值**：在AccessKey ID右侧输入对应的AccessKey Secret。

        **说明：** 建议您输入正确的AccessKey Secret。如果AccessKey Secret不正确，您将在RAM凭据首次轮转后获取一组新的AccessKey ID和AccessKey Secret。

    -   **描述信息**：输入RAM凭据的描述信息。
6.  在创建凭据对话框，选中**开启自动轮转**，配置**轮转周期**，然后单击**下一步**。

    **说明：** 如果无需自动轮转RAM凭据，请选择**关闭自动轮转**。

7.  在创建凭据对话框，审核凭据配置信息，单击**确认**。

8.  在创建成功对话框，单击**关闭**。

    您也可以单击**查看凭据详情**查看凭据信息。


## 删除动态RAM凭据

删除RAM凭据前，请确认该RAM凭据已不被使用。

您可以选择计划删除凭据和立即删除凭据两种方式，删除不需要的动态RAM凭据。删除动态RAM凭据不会删除RAM用户的AccessKey。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择RAM凭据托管的地域。

3.  在左侧导航栏，单击**凭据**。

4.  在目标RAM凭据右侧的**操作**列，选择**更多** \> **计划删除凭据**。

5.  在删除凭据对话框，选择凭据删除方式，然后单击**确定**。

    -   选择**计划删除凭据**，然后设置**预删除周期（7~30天）**。系统将在预删除周期后删除凭据。

        在预删除周期内，您可以还原凭据，取消删除操作。具体操作，请参见[还原动态RAM凭据](#section_orf_p66_q3p)。

    -   选择**立即删除凭据**，系统将立即删除凭据。

## 还原动态RAM凭据

当您选择了计划删除凭据的方式删除动态RAM凭据时，在预删除周期内，可以还原动态RAM凭据，取消删除操作。还原动态RAM凭据后，即可正常使用动态RAM凭据。

1.  登录[密钥管理服务控制台](https://kms.console.aliyun.com)。

2.  在页面左上角的地域下拉列表，选择RAM凭据托管的地域。

3.  在左侧导航栏，单击**凭据**。

4.  在目标RAM凭据右侧的**操作**列，选择**更多** \> **还原凭据**。

5.  在还原凭据对话框，单击**确定**。


