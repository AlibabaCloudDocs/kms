# Manage generic secrets

This topic describes how to use Alibaba Cloud CLI to manage generic secrets. You can also manage generic secrets in the Key Management Service \(KMS\) console or by calling API operations.

## Create a generic secret

-   Example 1: You do not specify a KMS customer master key \(CMK\) as the encryption key when you create a generic secret.

    Run the following command to call the [CreateSecret](/intl.en-US/API Reference/Secrets/CreateSecret.md) operation to create a generic secret. Secrets Manager uses the default CMK to encrypt the secret.

    ```
     aliyun kms CreateSecret \
        --SecretName db_cred \
        --SecretData "{\"uname\": \"alice\", \"pwd\": \"12****\"}" \
        --VersionId v1
    ```

    KMS returns the following results:

    ```
    {
      "Arn": "acs:kms:us-east-1:123456:secret/db_cred",
      "SecretName": "db_cred",
      "VersionId": "v1",
      "RequestId": "0993b6bb-08de-43b1-a93f-f7dbacaf****"
    }
    ```

-   Example 2: You specify a KMS CMK as the encryption key when you create a generic secret.

    Run the following command to call the [CreateSecret](/intl.en-US/API Reference/Secrets/CreateSecret.md) operation to create a generic secret. Secrets Manager uses the specified CMK to encrypt the secret.

    ```
     aliyun kms CreateSecret \
        --SecretName ssh_key \
        --SecretData ssh-key-blob \
        --VersionId v1 \
        --EncryptionKeyId Example-CMK-Id
    ```

    **Note:**

    -   Secrets Manager uses the specified CMK to generate a data key, which is used to encrypt the plaintext of the secret.
    -   If you want to specify a CMK when you create a generic secret by calling the CreateSecret operation, you must have the kms:GenerateDataKey permission.
    KMS returns the following results:

    ```
    {
        "Arn": "acs:kms:us-east-1:123456:secret/ssh_key",
        "SecretName": "ssh_key",
        "VersionId": "v1",
        "RequestId": "990bf04d-09a5-44de-925a-2da1fb43421d"
    }
    ```


## Querye generic secrets

Run the following command to call the [ListSecrets](/intl.en-US/API Reference/Secrets/ListSecrets.md) operation to query generic secrets:

```
aliyun kms ListSecrets    
```

KMS returns the following results:

```
{
    "SecretList": {
        "Secret": [
            {
                "SecretName": "db_cred",
                "CreateTime": "2020-01-22T03:55:18Z",
                "UpdateTime": "2020-01-22T03:55:18Z"
            },
            {
                "SecretName": "ssh_key",
                "CreateTime": "2020-01-22T03:57:09Z",
                "UpdateTime": "2020-01-22T03:57:09Z"
            }
        ]
    },
    "RequestId": "75aebbde-be68-4cab-ba6e-e4925b61****",
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 2
}
```

## Query the metadata of a generic secret

Run the following command to call the [DescribeSecret](/intl.en-US/API Reference/Secrets/DescribeSecret.md) operation to query the metadata of a generic secret:

```
aliyun kms DescribeSecret --SecretName ssh_key
```

KMS returns the following results:

```
{
    "Arn": "acs:kms:us-east-1:123456:secret/ssh_key",
    "SecretName": "ssh_key",
    "EncryptionKeyId": "Example-CMK-Id",
    "Description": "",
    "CreateTime": "2020-01-22T03:57:09Z",
    "UpdateTime": "2020-01-22T03:57:09Z",
    "RequestId": "ca61398f-e61e-4552-aa7e-957955f6125s"
}
```

## Delete a generic secret

-   Run the following command to call the [DeleteSecret](/intl.en-US/API Reference/Secrets/DeleteSecret.md) operation to delete a generic secret:
    -   By default, you can restore a secret within 30 days after the secret is deleted.

        ```
        aliyun kms DeleteSecret --SecretName ssh_key 
        ```

        KMS returns the following results:

        ```
        {
            "SecretName": "ssh_key",
            "RequestId": "3e54b02b-6461-46bb-afd5-dbd29d96eead",
            "PlannedDeleteTime": "2020-02-21T04:24:04.58616562Z"
        }
        ```

    -   When you delete a secret, you can set the period during which the secret can be restored to seven days.

        ```
        aliyun kms DeleteSecret --SecretName ssh_key --RecoveryWindowInDays 7
        ```

        KMS returns the following results:

        ```
        {
            "SecretName": "ssh_key",
            "RequestId": "95ec4f18-8f97-4fd5-b7c6-1588979dse4s",
            "PlannedDeleteTime": "2020-01-29T04:25:14.165242211Z"
        }
        ```

    -   You can forcibly delete a secret. The forcibly deleted secret cannot be restored.

        ```
        aliyun kms DeleteSecret --SecretName ssh_key --ForceDeleteWithoutRecovery true
        ```

        KMS returns the following results:

        ```
        {
            "SecretName": "ssh_key",
            "RequestId": "75efc9c3-8e21-4e38-b6e4-486886be1546",
            "PlannedDeleteTime": "2020-01-22T12:28:22.006884739+08:00"
        }
        ```

-   Run the following command to call the [RestoreSecret](/intl.en-US/API Reference/Secrets/RestoreSecret.md) operation to restore a secret within the period during which the secret can be restored.

    ```
    aliyun kms RestoreSecret --SecretName ssh_key  
    ```

    KMS returns the following results:

    ```
    {
        "RequestId": "12770cee-92af-42f5-88e0-cbaa7e0c1254",
        "SecretName": "ssh_key"
    }
    ```


## Rotate a generic secret

For more information about how to rotate a generic secret, see [Rotation of secrets](/intl.en-US/Secrets Manager/Generic Secrets/Rotation of secrets.md).

