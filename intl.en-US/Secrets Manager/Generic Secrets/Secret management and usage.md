# Secret management and usage

This topic describes the basic management and usage of secrets in KMS Secrets Manager and the related operations that you can perform on secrets.

## Basic scenario

This section takes a database username and its password as the managed secret.

![Basic Scenario](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/2940477951/p92891.png)

1.  A system administrator configures a username and its password in a database, which are used to access the database from the application MyApp.
2.  The administrator creates a secret object MyDbCreds in Secrets Manager to store the username and password.
3.  When MyApp needs to access the database, it sends a request for MyDbCreds to Secrets Manager.
4.  Secrets Manager reads the username and password in ciphertext, decrypts them, and returns the plaintext to MyApp by using HTTPS.
5.  MyApp reads and parses the plaintext returned by Secrets Manager to obtain the username and password and then uses them to access the database.

In this process, MyApp calls an API operation of Secrets Manager to obtain the username and password. This prevents the risk of information leakage caused by hardcoding the secret. The following figure shows the differences between hardcoding secrets and calling API operations of Secrets Manager.

![HardCodeVsSecretsManager](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3940477951/p92892.png)

## Manage and protect secrets

-   Example 1: You do not specify a KMS customer master key \(CMK\) as the encryption key when you create a secret.

    Run the following command-line interface \(CLI\) commands to create a secret. Secrets Manager uses its default encryption method to protect the secret value.

    ```
    $ aliyun kms CreateSecret \
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

-   Example 2: You specify a KMS CMK as the encryption key when you create a secret.

    Run the following CLI commands to create a secret. Secrets Manager uses the specified CMK to encrypt the secret.

    ```
    $ aliyun kms CreateSecret \
        --SecretName ssh_key \
        --SecretData ssh-key-blob \
        --VersionId v1 \
        --EncryptionKeyId Example-CMK-Id
    ```

    **Note:**

    -   Secrets Manager uses the specified CMK to generate a data key, which is used to encrypt the plaintext secret.
    -   The caller of CreateSecret must be granted the kms:GenerateDataKey permission on the specified CMK.
    KMS returns the following results:

    ```
    {
        "Arn": "acs:kms:us-east-1:123456:secret/ssh_key",
        "SecretName": "ssh_key",
        "VersionId": "v1",
        "RequestId": "990bf04d-09a5-44de-925a-2da1fb43****"
    }
    ```


## List secrets and view secret metadata

Call the [ListSecrets](/intl.en-US/API Reference/Secrets/ListSecrets.md) operation to list secrets.

```
$ aliyun kms ListSecrets                                                                                                                          
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

Call the [DescribeSecret](/intl.en-US/API Reference/Secrets/DescribeSecret.md) operation to view the metadata of a specific secret. This operation does not return the plaintext of the secret value.

```
$ aliyun kms DescribeSecret --SecretName ssh_key
{
    "Arn": "acs:kms:us-east-1:123456:secret/ssh_key",
    "SecretName": "ssh_key",
    "EncryptionKeyId": "Example-CMK-Id",
    "Description": "",
    "CreateTime": "2020-01-22T03:57:09Z",
    "UpdateTime": "2020-01-22T03:57:09Z",
    "RequestId": "ca61398f-e61e-4552-aa7e-957955f6****"
}
```

## Retrieve the plaintext of a secret value

Call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to retrieve the plaintext of a secret value encrypted by Secrets Manager.

```
$ aliyun kms GetSecretValue --SecretName db_cred                    
{
    "SecretName": "db_cred",
    "VersionId": "v1",
    "SecretData": "{\"uname\": \"alice\", \"pwd\": \"12****\"}",
    "SecretDataType": "text",
    "VersionStages": {
        "VersionStage": [
            "ACSCurrent"
        ]
    },
    "CreateTime": "2020-01-22T03:55:18Z",
    "RequestId": "06a380d8-a43c-4cd5-bdd4-e4a8e986****"
}
```

In the command output, the value of SecretData is the decrypted plaintext of the secret value.

**Note:** A secret object can store multiple versions, which are marked with stage labels. The initial version that is stored by calling CreateSecret is marked with ACSCurrent. By default, the GetSecretValue operation returns the secret value of the version that is marked with ACSCurrent.

## Delete and recover a secret

You can run the following command to delete a key without the need to specify a recovery period. By default, you can recover the key within 30 days.

```
$ aliyun kms DeleteSecret --SecretName ssh_key   
{
    "SecretName": "ssh_key",
    "RequestId": "3e54b02b-6461-46bb-afd5-dbd29d96****",
    "PlannedDeleteTime": "2020-02-21T04:24:04.58616562Z"
}
```

You can run the following command to delete a secret and set its recovery period to seven days:

```
$ aliyun kms DeleteSecret --SecretName ssh_key --RecoveryWindowInDays 7
{
    "SecretName": "ssh_key",
    "RequestId": "95ec4f18-8f97-4fd5-b7c6-1588979d****",
    "PlannedDeleteTime": "2020-01-29T04:25:14.165242211Z"
}
```

You can run the following command to recover a secret within its recovery period:

```
$ aliyun kms RestoreSecret --SecretName ssh_key                                                                                              
{
    "RequestId": "12770cee-92af-42f5-88e0-cbaa7e0c****",
    "SecretName": "ssh_key"
}
```

You can run the following command to forcibly delete a secret. After the secret is deleted, it cannot be recovered.

```
$ aliyun kms DeleteSecret --SecretName ssh_key --ForceDeleteWithoutRecovery true
{
    "SecretName": "ssh_key",
    "RequestId": "75efc9c3-8e21-4e38-b6e4-486886be****",
    "PlannedDeleteTime": "2020-01-22T12:28:22.006884739+08:00"
}
```

## Rotate a secret

For information about how to rotate a secret, see [Secret object model](/intl.en-US/Secrets Manager/Generic Secrets/Secret object model.md) and [Rotation of secrets](/intl.en-US/Secrets Manager/Generic Secrets/Rotation of secrets.md).

