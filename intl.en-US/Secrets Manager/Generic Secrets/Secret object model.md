# Secret object model

This topic describes the secret object model of KMS Secrets Manager. The model consists of the metadata, versions, and version stages of a secret.

To facilitate the rotation of secrets, Secrets Manager stores multiple versions of secret values in each secret object and marks the versions with stage labels. If you do not rotate a secret, Secrets Manager stores only one version in the secret object that corresponds to the secret. By default, Secrets Manager marks the first version as the "current version". The following figure shows a complete secret object model.

![Secret object](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1940477951/p92888.png)

## Secret metadata

Secret metadata has the following properties:

-   Secret name

    A secret name is used to specify a secret when you call an API operation of Secrets Manager.

-   Encryption key identifier

    Secrets Manager encrypts secrets to prevent their leakage. You can specify a KMS customer master key \(CMK\) or use the default encryption mode of Secrets Manager to implement encryption. For more information, see [Secure secret storage](/intl.en-US/Secrets Manager/Overview.md).

-   Description

    The description of a secret helps you manage secrets.

-   Resource tag

    Similar to other resources in KMS, secrets can also be managed by using tags.


## Secret versions

A secret object may contain multiple versions, which are marked with version numbers. Each secret value \(sensitive information\) that you put in a secret object is stored as a secret version. A secret version has the following features:

-   Secrets Manager encrypts the secret value of each version. Each secret value is specified by the `SecretData` parameter for the [CreateSecret](/intl.en-US/API Reference/Secrets/CreateSecret.md) or [PutSecretValue](/intl.en-US/API Reference/Secrets/PutSecretValue.md) operation and is encrypted and stored in the KMS server. You can call the [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md) operation to retrieve a plaintext secret value.
-   Each version number can only be written in a secret object once. You cannot use the [PutSecretValue](/intl.en-US/API Reference/Secrets/PutSecretValue.md) operation to modify the secret value of a version. If you store the same secret value by using the same version number multiple times, the effect is idempotent. If you store a new secret value by using an existing version number, the request is rejected.

## Version stages

The version stages in a secret object depend on which features of Secrets Manager you use.

-   If you only use Secrets Manager to manage a secret:

    The secret object has only one secret value and its version is "current version".

-   If you use Secrets Manager to manage and rotate a secret:

    A new secret value is stored in the secret object during rotation, and the new version becomes the "current version". Then, the "current version" obtained by the application that uses the secret is automatically updated.


In the preceding scenarios, the application that uses the secret only needs to obtain the secret value of the "current version". The "current version" is a version stage. Version stages are marked with stage labels. Secrets Manager has two built-in stage labels: **ACSCurrent** and **ACSPrevious**. ACSCurrent is used to mark the "current version", and ACSPrevious is used to mark the "previous version". Rules for the built-in stage labels are as follows:

-   There is only one "current version".

    The "current version" is marked with **ACSCurrent**. By default, when you call [GetSecretValue](/intl.en-US/API Reference/Secrets/GetSecretValue.md), the secret value of the version marked with **ACSCurrent** is returned.

-   The "current version" and "previous version" are updated automatically.

    If you call [PutSecretValue](/intl.en-US/API Reference/Secrets/PutSecretValue.md) to store a new secret value in a secret object without a specified version stage, the new version is marked with **ACSCurrent**.

    If you call [PutSecretValue](/intl.en-US/API Reference/Secrets/PutSecretValue.md) or [UpdateSecretVersionStage](/intl.en-US/API Reference/Secrets/UpdateSecretVersionStage.md) to update the version marked with **ACSCurrent**, the original version marked with **ACSCurrent** is marked with **ACSPrevious** and becomes the "previous version".


In addition to built-in stage labels **ACSCurrent** and **ACSPrevious**, you can use custom stage labels to mark extra version stages. The following rules apply to both built-in and custom stage labels:

-   One-to-one mapping rule

    Each stage label marks only one version. Each version may have zero, one, or more version stages.

-   Deprecating rule

    If a version is not marked with a stage label, it is put in a queue of versions to be deprecated. If the number of versions in a secret object exceeds the upper limit, the earliest version in the queue is deprecated.


