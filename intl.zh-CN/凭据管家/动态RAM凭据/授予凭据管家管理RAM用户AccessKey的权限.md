# 授予凭据管家管理RAM用户AccessKey的权限

当您使用凭据管家托管RAM凭据时，需要通过RAM服务角色为凭据管家授权，使凭据管家拥有管理RAM用户AccessKey的权限。本文为您介绍如何授予凭据管家管理RAM用户AccessKey的权限。

## 步骤一：创建自定义策略

1.  使用阿里云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏，选择**权限管理** \> **权限策略管理**。

3.  单击**创建权限策略**。

4.  设置**策略名称**为**AliyunKMSManagedRAMCrendentialsRolePolicy**。

5.  选择**配置模式**为**脚本配置**，然后在**策略内容**区域输入以下脚本。

    ```
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "ram:ListAccessKeys",
                    "ram:CreateAccessKey",
                    "ram:DeleteAccessKey",
                    "ram:UpdateAccessKey"
                ],
                "Resource": "*"
            }
        ],
        "Version": "1"
    }
    ```

6.  单击**确定**。


## 步骤二：创建RAM角色并授权

1.  使用阿里云账号登录[RAM控制台](https://ram.console.aliyun.com/)。

2.  在左侧导航栏，单击**RAM角色管理**。

3.  创建RAM角色。

    1.  单击**创建RAM角色**。

    2.  选择可信实体类型为**阿里云服务**，单击**下一步**。

    3.  选择角色类型为**普通服务角色**。

    4.  设置**角色名称**为**AliyunKMSManagedRAMCrendentialsRole**。

    5.  选择受信服务为**密钥管理服务**。

    6.  单击**完成**。

4.  为RAM角色授权。

    1.  单击**为角色授权**，被授权主体会自动填入。

    2.  在**添加权限**面板，选择**自定义策略**，然后选中权限策略**AliyunKMSManagedRAMCrendentialsRolePolicy**。

    3.  单击**确定**。

    4.  单击**完成**。


