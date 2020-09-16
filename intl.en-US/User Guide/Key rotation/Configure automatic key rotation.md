# Configure automatic key rotation

This topic describes how to configure automatic rotation of customer master keys \(CMKs\) in Key Management Service \(KMS\).

## Key versions

A CMK may have multiple key versions. Each key version represents an independently generated key. Key versions of the same CMK do not have any cryptographic relation to each other. KMS automatically rotates CMKs by generating new key versions.

**Types of key versions**

There are two types of key versions:

-   Primary key versions
    -   The primary key version of a CMK is an active encryption key. Each CMK has only one primary key version at any point in time.
    -   When you call an encryption API operation such as GenerateDataKey or Encrypt, KMS uses the primary key version of a specified CMK to encrypt the target plaintext.
    -   You can call the DescribeKey operation to query the PrimaryKeyVersion attribute.
-   Non-primary key versions
    -   A non-primary key version of a CMK is an inactive encryption key. Each CMK can have any number of non-primary key versions.
    -   Each non-primary key version was a primary key version and acted as the active encryption key in the past.
    -   When a new primary key version is created, KMS does not delete or disable non-primary key versions because they will be used to decrypt data.

**Note:** When you call an encryption API operation, the primary key version of a specified CMK is used. When you call a decryption API operation, the key version that was used to encrypt the ciphertext is used.

**Generation of key versions**

You can generate a key version in either of the following ways:

-   Create a CMK.

    You can call the CreateKey operation to create a CMK. If you set the Origin parameter to Aliyun\_KMS, KMS generates an initial key version and sets it as the primary key version.

-   Execute an automatic rotation policy.

    After you configure an automatic rotation policy, KMS executes the policy on a regular basis to generate new key versions.


## Automatic key rotation

**Configure and query an automatic rotation policy**

When you call the CreateKey operation to create a CMK, you can specify an automatic rotation policy for the CMK. You can call the UpdateRotationPolicy operation to update the current automatic rotation policy. When you call the API operations, you must configure the following parameters:

-   EnableAutomaticRotation: specifies whether to enable automatic rotation.
-   RotationInterval: indicates the time period for automatic rotation.

You can call the DescribeKey operation to view the configured automatic rotation policy. The following parameters are returned:

-   AutomaticRotation: indicates whether automatic rotation is enabled. For more information, see [Impact of CMK status on automatic rotation](#section_sij_bov_djx).
    -   Disabled: indicates that automatic rotation is disabled.
    -   Enabled: indicates that automatic rotation is enabled.
    -   Suspended: indicates that KMS suspends the execution of automatic rotation although automatic rotation is enabled.
-   RotationInterval: indicates the time period for automatic rotation.

**Execute an automatic rotation policy**

When automatic rotation is enabled, KMS calculates the time of the next rotation by using the following formula:

```
${NextRotationTime} = ${LastRotationTime} + ${RotationInterval}
```

where:

-   `LastRotationTime`: specifies the time the last key version is created. You can call the DescribeKey operation and check the `LastRotationDate` parameter to obtain the time.
-   `NextRotationTime`: specifies the time KMS performs the next rotation task to create a new key version. You can call the DescribeKey operation and check the `NextRotationDate` parameter to obtain the time.

**Note:** When you update the RotationInterval parameter of an automatic rotation policy, the value of NextRotationTime may be a point in time in the past. This does not affect the execution of the automatic rotation policy. If this situation occurs, KMS executes the automatic rotation policy immediately.

## Impacts of automatic rotation on encryption and decryption

After a CMK is rotated, KMS uses the current version of the CMK to encrypt data. For data that is encrypted by using a historical version of a CMK, you can use only the historical version to decrypt the data.

![Rotation1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5160220061/p166794.png)

You can call the ReEncrypt operation to decrypt the ciphertext that is encrypted by using a historical version of a CMK and encrypt the obtained plaintext data by using the current version of the CMK.

![Rotation2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/5160220061/p166798.png)

## Impact of CMK status on automatic rotation

A new key version can be created for a CMK only if this CMK is in the Enabled state \(the value of KeyState\). You must take note of the following points:

-   If a CMK is in the Disabled or Pending Deletion state, do not call the UpdateRotationPolicy operation to update its automatic rotation policy.
-   If a CMK enters the Disabled or Pending Deletion state after you enable automatic rotation for it, KMS suspends the execution of automatic rotation. In this case, if you call the DescribeKey operation, the returned value of the AutomaticRotation parameter is Suspended. When the CMK enters the Enabled state again, its automatic rotation policy becomes active.

## Limits

The following keys do not support multiple key versions:

-   Service-managed keys: the default keys managed by KMS for specific cloud services. These keys belong to the users of cloud services and are used to provide basic encryption protection for user data.
-   Keys based on BYOK: the keys that you imported to KMS. The Origin attribute of these keys is EXTERNAL. KMS does not generate key material or initiate rotation tasks for these keys. For more information about how to import key material, see [Import key material](/intl.en-US/User Guide/Use symmetric keys/Import key material.md).

These two types of keys do not support version-based manual or automatic key rotation. A BYOK-based key does not have multiple versions in KMS due to the following reasons:

-   Users have strong control over the persistence and lifecycle of BYOK-based keys. This makes management of the keys difficult and error-prone. For example, you must have on-premises key management facilities, data must be synchronized between on-premises facilities and the cloud, and no grace period is provided for key material deletion on the cloud. The complexity of maintaining multiple versions of BYOK-based keys makes key management much more risky.
-   Both primary and non-primary key versions may become unavailable at different points in time. For example, if key versions are deleted by KMS or imported again when they expire, CMKs may not be synchronized and encrypted data may not be decrypted by using the correct CMK. This affects system integrity.

