# Use RAM to authorize KMS resources {#concept_28953_zh .concept}

This topic describes the resource types, actions, and policy conditions in KMS. KMS uses RAM to control access to KMS resources.

An Alibaba Cloud account has full operation permissions on its own resources. RAM users and roles are granted varying operation permissions on resources through RAM authorization. Before you use RAM to authorize and access CMKs, make sure that you have read [../../SP\_65/DNRAM11820297/EN-US\_TP\_12331.dita\#concept\_oyr\_zzv\_tdb](../../SP_65/DNRAM11820297/EN-US_TP_12331.dita#concept_oyr_zzv_tdb) and [API overview](../../../../reseller.en-US/API Reference/API overview.md#).

## Resource types in KMS {#section_npt_5dp_kfb .section}

The following table lists all resource types and corresponding Alibaba Cloud Resource Names \(ARNs\) in KMS. They can be used in the Resource parameter of a RAM policy.

|Resource type|ARN|
|:------------|:--|
|Key container|acs:kms:$\{region\}:$\{account\}:key|
|Alias container|acs:kms:$\{region\}:$\{account\}:alias|
|Key|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|Alias|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## Actions in KMS {#section_dnf_c2p_kfb .section}

KMS defines actions used in RAM policies as access control for different API operations. They must be in the `kms:${api-name}` format.

**Note:** Access control is not required for the DescribeRegions operation. The DescribeRegions operation can be called by an Alibaba Cloud account, a RAM user, or a RAM role and authenticated directly.

The following table lists the relationship between KMS API operations, RAM actions, and resource types.

|KMS API operation|Action|Resource type|
|:----------------|:-----|:------------|
|ListKeys|kms:ListKeys|Key container|
|CreateKey|kms:CreateKey|Key container|
|DescribeKey|kms:DescribeKey|Key|
|EnableKey|kms:EnableKey|Key|
|DisableKey|kms:DisableKey|Key|
|ScheduleKeyDeletion|kms:ScheduleKeyDeletion|Key|
|CancelKeyDeletion|kms:CancelKeyDeletion|Key|
|GetParametersForImport|kms:GetParametersForImport|Key|
|ImportKeyMaterial|kms:ImportKeyMaterial|Key|
|DeleteKeyMaterial|kms:DeleteKeyMaterial|Key|
|Encrypt|kms:Encrypt|Key|
|GenerateDataKey|kms:GenerateDataKey|Key|
|Decrypt|kms:Decrypt|Key|
|ListAliases|kms:ListAliases|Alias container|
|CreateAlias|kms:CreateAlias|Alias and key|
|UpdateAlias|kms:UpdateAlias|Alias and key|
|DeleteAlias|kms:DeleteAlias|Alias and key|
|ListAliasesByKeyId|kms:ListAliasesByKeyId|Key|
|TagResource|kms:TagResource|Key|
|UntagResource|kms:UntagResource|Key|
|ListResourceTags|kms:ListResourceTags|Key|

## Policy conditions in KMS {#section_sk5_2yr_6gn .section}

You can add conditions to RAM policies to control their access to KMS. RAM authentication will only be successful when the specified conditions are met. For example, you can use `acs:CurrentTime` to control the time period when a RAM policy is valid.

In addition to global conditions, you can use tags as filters to restrict the use of key-related API operations such as Encrypt, Decrypt, and GenerateDataKey. Filters must be in the `kms:tag/${tag-key}` format.

For more information, see [Policy elements](../../../../reseller.en-US/User Guide/Policies/Policy language/Policy elements.md#).

## Common RAM policy examples {#section_bwj_tqo_cze .section}

-   The RAM policy allowing users to access all KMS resources

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

-   The RAM policy allowing users to view keys, aliases, and key usage permissions

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

-   The RAM policy allowing users to perform operations on keys that contain the following tag:

    -   Tag key: `Project`
    -   Tag value: `Apollo`
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


