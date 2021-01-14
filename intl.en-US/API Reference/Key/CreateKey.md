# CreateKey

Creates a CMK.

A CMK can be symmetric or asymmetric.

Symmetric CMKs are used to encrypt data of 6 KB or less and generate data keys to encrypt data larger than 6 KB. For more information, see [GenerateDataKey](~~28948~~).

Asymmetric CMKs are used to encrypt, decrypt, and sign data, and verify signatures, but cannot be used to generate data keys.

The following table lists the key types and operations supported by symmetric and asymmetric CMKs.

| |Key type

|Description

|Encryption and decryption

|Signature and verification |
|--|----------|-------------|---------------------------|----------------------------|
|Symmetric CMK

|Aliyun\_AES\_256

|AES key with a length of 256 bits

|Supported

|Unsupported |
|Symmetric CMK

|Aliyun\_SM4

|SM4 key

|Supported

|Unsupported |
|Asymmetric CMK

|RSA\_2048

|RSA key with a length of 2048 bits

|Supported

|Supported |
|Asymmetric CMK

|EC\_P256

|NIST-recommended elliptic curve P-256 \(secp256r1\)

|Not supported

|Supported |
|Asymmetric CMK

|EC\_P256K

|SECC elliptic curve secp256k1

|Not supported

|Supported |
|Asymmetric CMK

|EC\_SM2

|256-bit elliptic curve in the prime number domain defined by GBT32918

|Supported

|Supported |

**Note:**

-   The symmetric key KeySpec is prefixed with the standard key type`Aliyun_` which indicates the cryptographic algorithm that uses the standard key, but generates non-standard ciphertext. Asymmetric keys generate standard ciphertext or signatures.
-   An RSA key supports the ENCRYPT/DECRYPT operations or SIGN/VERIFY operations.
-   SM4 and SM2 are cryptographic algorithms approved by state cryptography Administration of China. KMS supports SM4 and SM2 through managed hardware security module deployed in mainland China.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateKey&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Scenario|Required|Example|Description|
|---------|--------|--------|-------|-----------|
|Action|String|Retained|CreateKey|The operation that you want to perform. Set the value to CreateKey. |
|Description|String|No|key description example|The description of the CMK.

The description can be up to 8,192 characters in length. |
|KeySpec|String|No|Aliyun\_AES\_256|The type of the CMK. Valid values:

-   Aliyun\_AES\_256
-   Aliyun\_SM4
-   RSA\_2048
-   EC\_P256
-   EC\_P256K
-   EC\_SM2

**Note:** If the CMK is created in a managed hardware security module in mainland China, the default value is Aliyun\_SM4. In other cases, the default value is Aliyun\_AES\_256. |
|KeyUsage|String|No|ENCRYPT/DECRYPT|The purpose of the CMK. Valid values:

-   ENCRYPT/DECRYPT: data encryption and decryption.
-   SIGN/VERIFY: generate and VERIFY a digital signature. |
|Origin|String|No|Aliyun\_KMS|The source of the key material. Valid values:

-   Aliyun\_KMS \(default\)
-   EXTERNAL

**Note:**

-   The value of this parameter is case-sensitive.
-   When KeySpec is an asymmetric key type, the EXTERNAL parameter cannot be selected.
-   If you select EXTERNAL, you must [import key material](~~68523~~). |
|ProtectionLevel|String|No|SOFTWARE|The protection level of the CMK. Valid values:

-   SOFTWARE \(default\)
-   HSM

**Note:**

-   The value of this parameter is case-sensitive.
-   When you set this parameter to HSM: If you set the Origin parameter to Aliyun\_KMS, the CMK is generated in the managed hardware security module. If you set the Origin parameter to externa, you can import external keys to a managed hardware security module for password calculation. |
|EnableAutomaticRotation|Boolean|No|false|Indicates whether automatic key rotation is enabled. Valid values:

-   true
-   false

**Note:** If the Origin parameter is set to EXTERNAL, or the KeySpec parameter is set to an asymmetric CMK type, automatic rotation is unavailable. |
|RotationInterval|String|No|365d|The period of automatic key rotation. It must be in the integer\[unit\] format. The unit can be d \(day\), h \(hour\), m \(minute\), or s \(second\). 7d or 604,800 S indicates a 7-day period. Valid values: 7 to 730 days.

**Note:** If EnableAutomaticRotation is set to true, this parameter is required. If not, this parameter is ignored. |

## Response parameters

|Parameter|Scenario|Example|Description|
|---------|--------|-------|-----------|
|KeyMetadata|Struct| |The metadata of the CMK. |
|Arn|String|acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the CMK. |
|AutomaticRotation|String|Enabled|Indicates whether automatic key rotation is enabled. Valid values:

-   Enabled: Automatic rotation is enabled.
-   Disabled: Automatic rotation is disabled.
-   Suspended: KMS suspended the execution of automatic key rotation. For more information, see [Automatic key rotation](~~134270~~).

**Note:** This API is only applicable to symmetric cmks. Asymmetric cmks do not support automatic rotation. |
|CreationDate|String|2016-03-25T10:42:40Z|The date and time the CMK was created. The time is displayed in UTC. |
|Creator|String|123456|The creator of the CMK. |
|DeleteDate|String|2020-07-06T18:22:03Z|The scheduled deletion time of the CMK.

For more information, see [ScheduleKeyDeletion](~~44196~~).

**Note:** This value is only returned when the KeyState value is PendingDeletion. |
|Description|String|key description example|The description of the CMK. |
|KeyId|String|08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|The globally unique ID of the CMK. |
|KeySpec|String|Aliyun\_AES\_256|The type of the CMK. |
|KeyState|String|Enabled|The status of the CMK.

For more information, see [impact of CMK states on API calls](~~44211~~). |
|KeyUsage|String|ENCRYPT/DECRYPT|The purpose of the CMK. |
|LastRotationDate|String|2019-06-06T18:22:03Z|The date and time the last rotation was performed. The time is displayed in UTC.

For a newly created key, the value of this parameter is the date and time the initial version of the new key was generated. |
|MaterialExpireTime|String|2020-07-06T18:22:03Z|The date and time the key material for the CMK expires. The time is displayed in UTC.

If the value is empty, the key material for the CMK does not expire. |
|NextRotationDate|String|2020-07-06T18:22:03Z|The time the next rotation is scheduled for execution.

**Note:** This value is only returned when AutomaticRotation is Enabled or Suspended. |
|Origin|String|Aliyun\_KMS|The source of the key material. |
|PrimaryKeyVersion|String|0ec2d249-9f64-4d8f-9587-1215525e\*\*\*\*|The ID of the current primary key version.

**Note:**

-   The primary key version is an active encryption key of a symmetric CMK, and key management uses the primary key version to process encryption requests.
-   This operation is not applicable to asymmetric cmks. |
|ProtectionLevel|String|SOFTWARE|The protection level of the CMK. |
|RotationInterval|String|31536000s|The period of automatic key rotation. Unit: seconds. Format: integer\[s\] For example, a 7-day rotation cycle is 604800 seconds. This value is only returned when AutomaticRotation is Enabled or Suspended. |
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|The ID of the instance. |

## Samples

Sample requests

```
https://[Endpoint]/?Action=CreateKey
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <KeyMetadata>
        <CreationDate>2016-03-25T10:42:40Z</CreationDate>
        <Description>key description example</Description>
        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</KeyId>
        <KeySpec>Aliyun_AES_256</KeySpec>
        <KeyState>Enabled</KeyState>
        <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
        <PrimaryKeyVersion>0ec2d249-9f64-4d8f-9587-1215525e****</PrimaryKeyVersion>
        <DeleteDate></DeleteDate>
        <Creator>123456</Creator>
        <Arn>acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</Arn>
        <Origin>Aliyun_KMS</Origin>
        <MaterialExpireTime></MaterialExpireTime>
        <ProtectionLevel>SOFTWARE</ProtectionLevel>
        <LastRotationDate>2016-03-25T10:42:40Z</LastRotationDate>
        <AutomaticRotation>Enabled</AutomaticRotation>
        <RotationInterval>31536000s</RotationInterval>
        <NextRotationDate>2017-03-25T10:42:40Z</NextRotationDate>
    </KeyMetadata>
    <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` format

```
{
        "KeyMetadata": {
                "CreationDate": "2016-03-25T10:42:40Z",
                "Description": "key description example",
                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
                "KeySpec": "Aliyun_AES_256",
                "KeyState": "Enabled",
                "KeyUsage": "ENCRYPT/DECRYPT",
                "PrimaryKeyVersion": "0ec2d249-9f64-4d8f-9587-1215525e****",
                "DeleteDate": "",
                "Creator":"123456",
                "Arn":"acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
                "Origin":"Aliyun_KMS",
                "MaterialExpireTime":"",
                "ProtectionLevel":"SOFTWARE",
                "LastRotationDate":"2016-03-25T10:42:40Z",
                "AutomaticRotation": "Enabled",
                "RotationInterval": "31536000s",
                "NextRotationDate":"2017-03-25T10:42:40Z"
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

