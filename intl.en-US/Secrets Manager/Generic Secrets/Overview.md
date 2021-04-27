# Overview

Generic secrets are basic secrets that are supported by Secrets Manager. You can use generic secrets to store sensitive data such as account passwords, AccessKey secrets, OAuth secrets and tokens, and API keys. A generic secret can have multiple versions so that you can update the secret value.

## Understand generic secrets

A generic secret consists of the metadata, secret versions, and stage labels that mark the secret versions.

![Secret](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/9003949161/p268678.png)

|Component|Description|
|---------|-----------|
|Metadata|The metadata of a secret contains the following parts:-   The name of the secret, which is used to specify the secret when you call an API operation of Secrets Manager.
-   The identifier of the encryption key, which is used to specify the identifier of your user-managed customer master key \(CMK\).
-   Other data, such as description and resource tags. |
|Secret versions|Each secret value that you write into a secret is stored as a secret version. The secret value is sensitive data. You can read the secret value of a secret version based on the secret name and version number. Each secret version that is identified by the version number can be written into a secret only once and cannot be modified.|
|Stage labels|Secret versions are marked with stage labels and can be referenced by using stage labels. Secrets Manager has two built-in stage labels: **ACSCurrent** and **ACSPrevious**. By default, you can call the [PutSecretValue](/intl.en-US/API Reference/Secrets/PutSecretValue.md) operation to mark the newly stored secret version with **ACSCurrent**. Then, you can call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to read the secret version that is marked with **ACSCurrent**. You can also customize stage labels. **Note:** A stage label is similar to a pointer and follows these principles:

-   Each stage label marks only one version. Each version may have zero to multiple stage labels.
-   If the number of versions in a secret exceeds the upper limit, the earliest version that is not marked with a stage label is deleted. |

## Use generic secrets

You can use generic secrets in the following way:

-   [Manage generic secrets](/intl.en-US/Secrets Manager/Generic Secrets/Manage generic secrets.md)
-   [Rotate generic secrets](/intl.en-US/Secrets Manager/Generic Secrets/Rotate generic secrets.md)
-   [Allow applications to access Secrets Manager](/intl.en-US/Secrets Manager/Allow applications to access Secrets Manager.md)

