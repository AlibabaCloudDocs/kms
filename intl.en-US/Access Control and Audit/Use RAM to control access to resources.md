# Use RAM to control access to resources

Key Management Service \(KMS\) uses Resource Access Management \(RAM\) to control access to resources. This topic describes the resource types, actions, and policy conditions in KMS.

Alibaba Cloud accounts have full operation permissions on their own resources. RAM users and RAM roles are granted operation permissions on resources based on explicit RAM authorization.

Before you use RAM to grant access to customer master keys \(CMKs\), make sure that you have read the following topics:

-   [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)
-   [List of operations by function](/intl.en-US/API Reference/API Reference (RAM)/List of operations by function.md)

## Resource types in KMS

The following table describes all resource types and corresponding Alibaba Cloud Resource Names \(ARNs\) in KMS. They can be used in the Resource parameter of a RAM policy.

|Resource type|ARN|
|:------------|:--|
|Abstract key container|acs:kms:$\{region\}:$\{account\}:key|
|Abstract secret container|acs:kms:$\{region\}:$\{account\}:secret|
|Abstract alias container|acs:kms:$\{region\}:$\{account\}:alias|
|Key|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|Secret|acs:kms:$\{region\}:$\{account\}:secret/$\{secret-name\}|
|Alias|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## Actions in KMS

KMS defines actions used in RAM policies for each API operation that requires access control. Actions must be in the `kms:<api-name>` format.

**Note:** The DescribeRegions operation requires no access control. It can be called by Alibaba Cloud accounts, RAM users, or RAM roles after they pass authentication.

The following table describes the RAM actions and resource types that correspond to each KMS API operation.

-   Key API operations

    |Operation|Action|Resource type|
    |:--------|:-----|:------------|
    |ListKeys|kms:ListKeys|Abstract key container|
    |CreateKey|kms:CreateKey|Abstract key container|
    |DescribeKey|kms:DescribeKey|Key|
    |UpdateKeyDescription|kms:UpdateKeyDescription|Key|
    |EnableKey|kms:EnableKey|Key|
    |DisableKey|kms:DisableKey|Key|
    |ScheduleKeyDeletion|kms:ScheduleKeyDeletion|Key|
    |CancelKeyDeletion|kms:CancelKeyDeletion|Key|
    |GetParametersForImport|kms:GetParametersForImport|Key|
    |ImportKeyMaterial|kms:ImportKeyMaterial|Key|
    |DeleteKeyMaterial|kms:DeleteKeyMaterial|Key|
    |ListAliases|kms:ListAliases|Abstract alias container|
    |CreateAlias|kms:CreateAlias|Alias and key|
    |UpdateAlias|kms:UpdateAlias|Alias and key|
    |DeleteAlias|kms:DeleteAlias|Alias and key|
    |ListAliasesByKeyId|kms:ListAliasesByKeyId|Key|
    |CreateKeyVersion|kms:CreateKeyVersion|Key|
    |DescribeKeyVersion|kms:DescribeKeyVersion|Key|
    |ListKeyVersions|kms:ListKeyVersions|Key|
    |UpdateRotationPolicy|kms:UpdateRotationPolicy|Key|
    |Encrypt|kms:Encrypt|Key|
    |Decrypt|kms:Decrypt|Key|
    |ReEncrypt|    -   kms:ReEncryptFrom
    -   kms:ReEncryptTo
    -   kms:ReEncrypt\*
|Key|
    |GenerateDataKey|kms:GenerateDataKey|Key|
    |GenerateDataKeyWithoutPlaintext|kms:GenerateDataKeyWithoutPlaintext|Key|
    |ExportDataKey|kms:ExportDataKey|Key|
    |GenerateAndExportDataKey|kms:GenerateAndExportDataKey|Key|
    |AsymmetricSign|kms:AsymmetricSign|Key|
    |AsymmetricVerify|kms:AsymmetricVerify|Key|
    |AsymmetricEncrypt|kms:AsymmetricEncrypt|Key|
    |AsymmetricDecrypt|kms:AsymmetricDecrypt|Key|
    |GetPublicKey|kms:GetPublicKey|Key|

-   Secrets Manager API operations

    |Operation|Action|Resource type|
    |---------|------|-------------|
    |CreateSecret|kms:CreateSecret|Abstract secret container|
    |ListSecrets|kms:ListSecrets|Abstract secret container|
    |DescribeSecret|kms:DescribeSecret|Secret|
    |DeleteSecret|kms:DeleteSecret|Secret|
    |UpdateSecret|kms:UpdateSecret|Secret|
    |RestoreSecret|kms:RestoreSecret|Secret|
    |GetSecretValue|    -   kms:GetSecretValue
    -   kms:Decrypt
**Note:** The permission on kms:Decrypt is required only when a user-defined CMK is specified as the encryption key for a generic secret.

|Secret|
    |PutSecretValue|    -   kms:PutSecretValue
    -   kms:GenerateDataKey
**Note:** The permission on kms:GenerateDataKey is required only when a user-defined CMK is specified as the encryption key for a generic secret.

|Secret|
    |ListSecretVersionIds|kms:ListSecretVersionIds|Secret|
    |UpdateSecretVersionStage|kms:UpdateSecretVersionStage|Secret|
    |GetRandomPassword|kms:GetRandomPassword|N/A|

-   Tag management API operations

    |Operation|Action|Resource type|
    |---------|------|-------------|
    |ListResourceTags|kms:ListResourceTags|Key or secret|
    |UntagResource|kms:UntagResource|Key or secret|
    |TagResource|kms:TagResource|Key or secret|


## Policy conditions in KMS

You can add conditions to RAM policies to control access to KMS. RAM authentication will be successful only when the specified conditions are met. For example, you can use `acs:CurrentTime` to control the time period when a RAM policy is valid.

In addition to global conditions, you can use tags as filters to limit the use of cryptographic API operations such as Encrypt, Decrypt, and GenerateDataKey. Tag keys must be specified in the format of `kms:tag/<tag-key>`.

For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

## RAM policy examples

-   A RAM policy that allows users to access all KMS resources

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

-   A RAM policy that allows users to query keys and aliases and use keys

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

-   A RAM policy that allows users to use only keys with the following tag:

    -   Tag key: `Project`
    -   Tag value: `Apollo`
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


