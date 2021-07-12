# Use RAM to control access to KMS resources

Key Management Service \(KMS\) implements access control by using Resource Access Management \(RAM\) policies. This topic describes the KMS resource types, actions, and conditions that can be defined in RAM policies.

Alibaba Cloud accounts have full operation permissions on their own resources. RAM users and roles are granted operation permissions on resources after explicit authorization.

Before you can use RAM to perform authorization and access customer master keys \(CMKs\), read the following topics:

-   [What is RAM?](/intl.en-US/Product Introduction/What is RAM?.md)
-   [List of operations by function](/intl.en-US/API Reference/API Reference (RAM)/List of operations by function.md)

## Resource types in KMS

The following table describes all resource types and their Alibaba Cloud Resource Names \(ARNs\) in KMS. The ARNs can be used in the Resource parameter of a RAM policy.

|Resource type|ARN|
|:------------|:--|
|Key container|acs:kms:$\{region\}:$\{account\}:key|
|Secret container|acs:kms:$\{region\}:$\{account\}:secret|
|Alias container|acs:kms:$\{region\}:$\{account\}:alias|
|Key|acs:kms:$\{region\}:$\{account\}:key/$\{key-id\}|
|Secret|acs:kms:$\{region\}:$\{account\}:secret/$\{secret-name\}|
|Alias|acs:kms:$\{region\}:$\{account\}:alias/$\{alias-name\}|

## Actions in KMS

KMS defines actions used in RAM policies for each API operation that requires access control. In most cases, actions are in the `kms:<api-name>` format.

**Note:** The DescribeRegions operation does not require access control. It can be called by Alibaba Cloud accounts, RAM users, or RAM roles after they pass RAM authentication.

The following tables list the RAM actions and resource types that correspond to each KMS API operation.

-   Key API operations

    |Operation|Action|Resource type|
    |:--------|:-----|:------------|
    |ListKeys|kms:ListKeys|Key container|
    |CreateKey|kms:CreateKey|Key container|
    |DescribeKey|kms:DescribeKey|Key|
    |UpdateKeyDescription|kms:UpdateKeyDescription|Key|
    |EnableKey|kms:EnableKey|Key|
    |DisableKey|kms:DisableKey|Key|
    |ScheduleKeyDeletion|kms:ScheduleKeyDeletion|Key|
    |CancelKeyDeletion|kms:CancelKeyDeletion|Key|
    |GetParametersForImport|kms:GetParametersForImport|Key|
    |ImportKeyMaterial|kms:ImportKeyMaterial|Key|
    |DeleteKeyMaterial|kms:DeleteKeyMaterial|Key|
    |ListAliases|kms:ListAliases|Alias container|
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
    |CreateSecret|kms:CreateSecret|Secret container|
    |ListSecrets|kms:ListSecrets|Secret container|
    |DescribeSecret|kms:DescribeSecret|Secret|
    |DeleteSecret|kms:DeleteSecret|Secret|
    |UpdateSecret|kms:UpdateSecret|Secret|
    |RestoreSecret|kms:RestoreSecret|Secret|
    |GetSecretValue|    -   kms:GetSecretValue
    -   kms:Decrypt
**Note:** The permissions on kms:Decrypt are required only when a user-managed CMK is specified as the encryption key for a generic secret.

|Secret|
    |PutSecretValue|    -   kms:PutSecretValue
    -   kms:GenerateDataKey
**Note:** The permissions on kms:GenerateDataKey are required only when a user-managed CMK is specified as the encryption key for a generic secret.

|Secret|
    |ListSecretVersionIds|kms:ListSecretVersionIds|Secret|
    |UpdateSecretVersionStage|kms:UpdateSecretVersionStage|Secret|
    |GetRandomPassword|kms:GetRandomPassword|None|

-   Tag management API operations

    |Operation|Action|Resource type|
    |---------|------|-------------|
    |ListResourceTags|kms:ListResourceTags|Key or secret|
    |UntagResource|kms:UntagResource|Key or secret|
    |TagResource|kms:TagResource|Key or secret|


## Policy conditions in KMS

You can add conditions in RAM policies to control access to KMS. RAM authentication succeeds only when the added conditions are met. For example, you can add an `acs:CurrentTime` condition to control the period during which a RAM policy is valid.

In addition to global conditions, you can use tags as filters to limit the use of cryptographic API operations, such as Encrypt, Decrypt, and GenerateDataKey. Filters must be in the `kms:tag/<tag-key>` format.

For more information, see [Policy elements](/intl.en-US/Policy Management/Policy language/Policy elements.md).

## Examples of RAM policies

-   RAM policy that allows users to access all KMS resources

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

-   RAM policy that allows users only to query keys, aliases, and permissions to use keys

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

-   RAM policy that allows users to use keys that contain the following tag to perform cryptographic operations:

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

-   RAM policy that allows users only to query secrets, versions and content of secrets, and permissions to generate random passwords

    ```
    {
      "Version": "1",
      "Statement": [
        {
          "Effect": "Allow",
          "Action": [
            "kms:List*", "kms:Describe*",
            "kms:GetSecretValue", "kms:Decrypt", "kms:GetRandomPassword"
          ],
          "Resource": [
            "*"
          ]
        }
      ]
    }         
    ```


