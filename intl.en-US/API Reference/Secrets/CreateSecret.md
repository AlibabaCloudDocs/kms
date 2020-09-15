# CreateSecret

Creates a secret and stores the secret value in the initial version.

You must specify the secret name, the secret value stored in the initial version, and the version number. The initial version is marked with **ACSCurrent**.

You can specify a symmetric CMK as the encryption key that is used to protect the secret. If you do not specify a CMK, Secrets Manager creates an encryption key to encrypt the secrets that are created by using your Alibaba Cloud account in the current region. Secrets Manager encrypts only the secret value of each version. It does not encrypt the metadata, such as the secret name, version number, and state label.

To use a specified CMK to encrypt a secret value, you must be granted the `kms:GenerateDataKey` permission on the CMK.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateSecret|The operation that you want to perform. Set the value to CreateSecret. |
|SecretData|String|Yes|\{"user":"root","passwd":"\*\*\*\*"\}|The value of the secret that you want to create. Secrets Manager encrypts the secret value and stores it in the initial version. |
|SecretName|String|Yes|mydbconninfo|The name of the secret. |
|VersionId|String|Yes|v1|The version number of the initial version. Version numbers are unique in each secret object. |
|EncryptionKeyId|String|No|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|The ID of the KMS CMK that is used to encrypt the secret value.

If you do not specify this parameter, Secrets Manager automatically creates an encryption key to encrypt the secret.

**Note:** The KMS CMK must be a symmetric key. |
|SecretDataType|String|No|text|The type of the secret value. Valid values:

-   text
-   binary |
|Description|String|No|mydbinfo|The description of the secret. |
|Tags|String|No|\[\{\\"TagKey\\":\\"key1\\",\\"TagValue\\":\\"val1\\"\},\{\\"TagKey\\":\\"key2\\",\\"TagValue\\":\\"val2\\"\}\]|The tag of the secret. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:test-1:127046163668\*\*\*\*:secret/seret001|The Alibaba Cloud Resource Name \(ARN\). |
|RequestId|String|2c124f6f-4210-499f-b88a-69f54004d2d8|The ID of the request. |
|SecretName|String|mydbconninfo|The name of the secret. |
|VersionId|String|v1|The version number of the idempotent operation. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CreateSecret
&SecretData={"user":"root","passwd":"****"}
&SecretDataType=text
&SecretName=mydbconninfo
&VersionId=v1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
          <Arn>acs:kms:test-1:127046163668****:secret/secret001</Arn>
          <SecretName>mydbconninfo</SecretName>
          <VersionId>v1</VersionId>
          <RequestId>2c124f6f-4210-499f-b88a-69f54004d2d8</RequestId>
</KMS>
```

`JSON` format

```
{
    "Arn": "acs:kms:test-1:127046163668****:secret/secret001",
    "SecretName": "mydbconninfo",
    "VersionId": "v1",
    "RequestId": "2c124f6f-4210-499f-b88a-69f54004d2d8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

