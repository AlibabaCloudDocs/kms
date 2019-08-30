# 使用RAM实现访问控制 {#concept_28953_zh .concept}

密钥管理服务（KMS）通过访问控制（RAM）实现对资源的访问控制。本文为您介绍KMS定义的资源类型、操作和策略条件。

云帐号对自己的资源拥有完整的操作权限，RAM用户和角色则需要通过显示授权获取对应资源的操作权限。在了解如何使用RAM授权和访问主密钥之前，请确保您已详细阅读了[什么是访问控制](../../../../intl.zh-CN/产品简介/什么是访问控制.md#)和[API概览](../../../../intl.zh-CN/API参考（RAM）/API概览.md#)。

## KMS定义的资源类型 {#section_npt_5dp_kfb .section}

下表列出了KMS定义的所有资源类型以及对应的资源名称（ARN），用于RAM权限策略的Resource元素。

|资源类型|ARN|
|:---|:--|
|抽象密钥容器|acs:kms:$\{region\}:$\{account\}:key|
|抽象别名容器|acs:kms:$\{region\}:$\{account\}:alias|
|密钥|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|别名|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## KMS定义的操作 {#section_dnf_c2p_kfb .section}

针对每一个需要进行访问控制的接口，KMS都定义了用于RAM权限策略的操作（Action），通常为`kms:${api-name}`。

**说明：** DescribeRegions不需要进行访问控制，只要请求可以通过认证校验，便可以调用。调用者可以是云帐号、RAM用户或RAM角色。

下表列出了KMS接口的对应RAM Action，以及接口所访问的资源类型。

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
|Encrypt|kms:Encrypt|密钥|
|GenerateDataKey|kms:GenerateDataKey|密钥|
|GenerateDataKeyWithoutPlaintext|kms:GenerateDataKeyWithoutPlaintext|密钥|
|Decrypt|kms:Decrypt|密钥|
|ListAliases|kms:ListAliases|抽象别名容器|
|CreateAlias|kms:CreateAlias|别名，密钥|
|UpdateAlias|kms:UpdateAlias|别名，密钥|
|DeleteAlias|kms:DeleteAlias|别名，密钥|
|ListAliasesByKeyId|kms:ListAliasesByKeyId|密钥|
|TagResource|kms:TagResource|密钥|
|UntagResource|kms:UntagResource|密钥|
|ListResourceTags|kms:ListResourceTags|密钥|
|CreateKeyVersion|kms:CreateKeyVersion|密钥|
|DescribeKeyVersion|kms:DescribeKeyVersion|密钥|
|ListKeyVersions|kms:ListKeyVersions|密钥|
|UpdateRotationPolicy|kms:UpdateRotationPolicy|密钥|

## KMS支持的策略条件 {#section_sk5_2yr_6gn .section}

您可以在RAM权限策略中设定条件控制对KMS的访问，只有当条件满足时，权限验证才能通过。例如，用户可以使用`acs:CurrentTime`条件限制权限策略有效的时间。

除了阿里云全局条件，您也可以使用标签作为条件关键字，限制对Encrypt、Decrypt、GenerateDataKey等密码运算API的使用。条件关键字的格式为`kms:tag/${tag-key}`。

详情请参见[Policy 基本元素](../../../../intl.zh-CN/用户指南/权限策略/权限策略语言/权限策略基本元素.md#)。

## 常见的授权策略示例 {#section_bwj_tqo_cze .section}

-   允许访问所有的KMS资源

    ``` {#codeblock_jga_vzj_tdc}
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

-   只读访问权限，即列出、查看密钥、查看别名与使用密钥权限

    ``` {#codeblock_u56_hm6_pg1}
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
    ``` {#codeblock_kf1_z3j_z76}
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


