# 使用RAM实现对资源的访问控制

密钥管理服务KMS（Key Management Service）通过访问控制RAM（Resource Access Management）实现对资源的访问控制。本文为您介绍KMS定义的资源类型、操作和策略条件。

阿里云账号对自己的资源拥有完整的操作权限，RAM用户和RAM角色则需要通过显示授权获取对应资源的操作权限。

在了解如何使用RAM授权和访问主密钥之前，请了解以下内容：

-   [什么是访问控制](/cn.zh-CN/产品简介/什么是访问控制.md)
-   [API概览](/cn.zh-CN/API参考/API参考（RAM）/API概览.md)

## KMS定义的资源类型

下表列出了KMS定义的所有资源类型以及对应的资源名称（ARN），用于RAM权限策略的Resource元素。

|资源类型|ARN|
|:---|:--|
|抽象密钥容器|acs:kms:$\{region\}:$\{account\}:key|
|抽象凭据容器|acs:kms:$\{region\}:$\{account\}:secret|
|抽象别名容器|acs:kms:$\{region\}:$\{account\}:alias|
|密钥|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|凭据|acs:kms:$\{region\}:$\{account\}:secret/$\{secret-name\}|
|别名|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## KMS定义的操作

针对每一个需要进行访问控制的接口，KMS都定义了用于RAM权限策略的操作（Action），通常为`kms:${api-name}`。

**说明：** DescribeRegions不需要进行访问控制，只要请求可以通过认证校验，即可调用。调用者可以是阿里云账号、RAM用户或RAM角色。

以下表格列出了KMS接口的对应RAM权限策略操作，以及接口所访问的资源类型。

-   密钥服务接口

    |KMS接口|Action|资源类型|
    |:----|:-----|:---|
    |ListKeys|kms:ListKeys|抽象密钥容器|
    |CreateKey|kms:CreateKey|抽象密钥容器|
    |DescribeKey|kms:DescribeKey|密钥|
    |UpdateKeyDescription|kms:UpdateKeyDescription|密钥|
    |EnableKey|kms:EnableKey|密钥|
    |DisableKey|kms:DisableKey|密钥|
    |ScheduleKeyDeletion|kms:ScheduleKeyDeletion|密钥|
    |CancelKeyDeletion|kms:CancelKeyDeletion|密钥|
    |GetParametersForImport|kms:GetParametersForImport|密钥|
    |ImportKeyMaterial|kms:ImportKeyMaterial|密钥|
    |DeleteKeyMaterial|kms:DeleteKeyMaterial|密钥|
    |ListAliases|kms:ListAliases|抽象别名容器|
    |CreateAlias|kms:CreateAlias|别名和密钥|
    |UpdateAlias|kms:UpdateAlias|别名和密钥|
    |DeleteAlias|kms:DeleteAlias|别名和密钥|
    |ListAliasesByKeyId|kms:ListAliasesByKeyId|密钥|
    |CreateKeyVersion|kms:CreateKeyVersion|密钥|
    |DescribeKeyVersion|kms:DescribeKeyVersion|密钥|
    |ListKeyVersions|kms:ListKeyVersions|密钥|
    |UpdateRotationPolicy|kms:UpdateRotationPolicy|密钥|
    |Encrypt|kms:Encrypt|密钥|
    |Decrypt|kms:Decrypt|密钥|
    |ReEncrypt|    -   kms:ReEncryptFrom
    -   kms:ReEncryptTo
    -   kms:ReEncrypt\*
|密钥|
    |GenerateDataKey|kms:GenerateDataKey|密钥|
    |GenerateDataKeyWithoutPlaintext|kms:GenerateDataKeyWithoutPlaintext|密钥|
    |ExportDataKey|kms:ExportDataKey|密钥|
    |GenerateAndExportDataKey|kms:GenerateAndExportDataKey|密钥|
    |AsymmetricSign|kms:AsymmetricSign|密钥|
    |AsymmetricVerify|kms:AsymmetricVerify|密钥|
    |AsymmetricEncrypt|kms:AsymmetricEncrypt|密钥|
    |AsymmetricDecrypt|kms:AsymmetricDecrypt|密钥|
    |GetPublicKey|kms:GetPublicKey|密钥|

-   凭据管家接口

    |KMS 接口|Action|资源类型|
    |------|------|----|
    |CreateSecret|kms:CreateSecret|抽象凭据容器|
    |ListSecrets|kms:ListSecrets|抽象凭据容器|
    |DescribeSecret|kms:DescribeSecret|凭据|
    |DeleteSecret|kms:DeleteSecret|凭据|
    |UpdateSecret|kms:UpdateSecret|凭据|
    |RestoreSecret|kms:RestoreSecret|凭据|
    |GetSecretValue|kms:GetSecretValue|凭据|
    |PutSecretValue|kms:PutSecretValue|凭据|
    |ListSecretVersionIds|kms:ListSecretVersionIds|凭据|
    |UpdateSecretVersionStage|kms:UpdateSecretVersionStage|凭据|
    |GetRandomPassword|kms:GetRandomPassword|无|

-   标签管理接口

    |KMS 接口|Action|资源类型|
    |------|------|----|
    |ListResourceTags|kms:ListResourceTags|密钥或凭据|
    |UntagResource|kms:UntagResource|密钥或凭据|
    |TagResource|kms:TagResource|密钥或凭据|


## KMS支持的策略条件

您可以在RAM权限策略中设定条件控制对KMS的访问，只有当条件满足时，权限验证才能通过。例如，您可以使用`acs:CurrentTime`条件限制权限策略有效的时间。

除了阿里云全局条件，您也可以使用标签作为条件关键字，限制对Encrypt、Decrypt、GenerateDataKey等密码运算API的使用。条件关键字的格式为`kms:tag/${tag-key}`。

详情请参见[权限策略基本元素](/cn.zh-CN/权限策略管理/权限策略语言/权限策略基本元素.md)。

## 常见的授权策略示例

-   允许访问所有的KMS资源

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "kms:*"
          ],
          "Resource": [
            "*"
          ]
        }
      ]
    }               
    ```

-   只读访问权限，即列出和查看密钥、查看别名以及使用密钥权限

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "kms:List*", "kms:Describe*",
            "kms:Encrypt", "kms:Decrypt", "kms:GenerateDataKey"
          ],
          "Resource": [
            "*"
          ]
        }
      ]
    }             
    ```

-   允许使用含有下列标签的密钥进行密码运算：

    -   标签键：`Project`
    -   标签值：`Apollo`
    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "kms:Encrypt", "kms:Decrypt", "kms:GenerateDataKey"
                ],
                "Resource": [
                    "*"
                ],
                "Condition": {
                    "StringEqualsIgnoreCase": {
                        "kms:tag/Project": [
                            "Apollo"
                        ]
                    }
                }
            }
        ]
    }               
    ```


