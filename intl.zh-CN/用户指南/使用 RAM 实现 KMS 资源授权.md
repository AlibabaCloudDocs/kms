# 使用 RAM 实现 KMS 资源授权 {#concept_28953_zh .concept}

阿里云密钥管理服务（KMS）通过访问控制（RAM）实现对 KMS 资源的访问控制，本文档描述了 KMS 定义的资源类型、操作以及策略条件。

云帐号对自己的资源拥有完整的操作权限，RAM 用户和角色则需要通过显示授权获取到对资源的操作权限。在了解如何使用 RAM 来授权和访问主密钥之前，请确保您已详细阅读了[../../SP\_65/DNRAM11820297/ZH-CN\_TP\_12331\_V10.dita\#concept\_oyr\_zzv\_tdb](../../SP_65/DNRAM11820297/ZH-CN_TP_12331_V10.dita#concept_oyr_zzv_tdb) 和 [API 概览](../../../../intl.zh-CN/API参考（RAM）/API 概览.md#)。

## KMS 定义的资源类型 {#section_npt_5dp_kfb .section}

下表列出了 KMS 定义的所有资源类型以及对应的资源名称（ARN），用于 RAM 权限策略的 Resource 元素。

|资源类型|ARN|
|:---|:--|
|抽象密钥容器|acs:kms:$\{region\}:$\{account\}:key|
|抽象别名容器|acs:kms:$\{region\}:$\{account\}:alias|
|密钥|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|别名|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## KMS 定义的操作 {#section_dnf_c2p_kfb .section}

针对每一个需要进行访问控制的接口，KMS 都定义了用于 RAM 权限策略的操作（Action）：通常为：`kms:${api-name}`。

**说明：** DescribeRegions 不需要进行访问控制，只要请求可以通过认证校验就可以调用，调用者可以是云帐号，RAM 用户或角色。

下表列出了 KMS 接口的对应 RAM action，以及接口所访问的资源类型。

|KMS 接口|Action|资源类型|
|:-----|:-----|:---|
|ListKeys|kms:ListKeys|抽象密钥容器|
|CreateKey|kms:CreateKey|抽象密钥容器|
|DescribeKey|kms:DescribeKey|密钥|
|EnableKey|kms:EnableKey|密钥|
|DisableKey|kms:DisableKey|密钥|
|ScheduleKeyDeletion|kms:ScheduleKeyDeletion|密钥|
|CancelKeyDeletion|kms:CancelKeyDeletion|密钥|
|GetParametersForImport|kms:GetParametersForImport|密钥|
|ImportKeyMaterial|kms:ImportKeyMaterial|密钥|
|DeleteKeyMaterial|kms:DeleteKeyMaterial|密钥|
|Encrypt|kms:Encrypt|密钥|
|GenerateDataKey|kms:GenerateDataKey|密钥|
|Decrypt|kms:Decrypt|密钥|
|ListAliases|kms:ListAliases|抽象别名容器|
|CreateAlias|kms:CreateAlias|别名，密钥|
|UpdateAlias|kms:UpdateAlias|别名，密钥|
|DeleteAlias|kms:DeleteAlias|别名，密钥|
|ListAliasesByKeyId|kms:ListAliasesByKeyId|密钥|
|TagResource|kms:TagResource|密钥|
|UntagResource|kms:UntagResource|密钥|
|ListResourceTags|kms:ListResourceTags|密钥|

## KMS 支持的策略条件 {#section_sk5_2yr_6gn .section}

您可以在 RAM 权限策略中设定条件控制对 KMS 的访问，只有当条件满足时，权限验证才能通过。例如：用户可以使用`acs:CurrentTime`条件限制权限策略有效的时间。

除了阿里云全局条件，您也可以使用标签作为条件关键字，来限制对 Encrypt、Decrypt、GenerateDataKey 等密码运算 API 的使用。条件关键字的格式为`kms:tag/${tag-key}`。

详情请参考：[Policy 基本元素](../../../../intl.zh-CN/用户指南/权限管理/Policy 语言/Policy 基本元素.md#)。

## 常见的授权策略示例 { .section}

-   允许访问所有的 KMS 资源

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

-   只读访问权限，即列出、查看密钥、查看别名与使用密钥权限。

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

-   允许使用具有下列标签的密钥进行密码运算：

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


