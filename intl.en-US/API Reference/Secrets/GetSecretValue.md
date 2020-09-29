# GetSecretValue

Obtains a secret value.

-   If you do not specify a version number or stage label, Secrets Manager returns the secret value of the version marked with **ACSCurrent**.
-   If a KMS customer master key \(CMK\) is specified to encrypt the secret value, you must be granted the `kms:Decrypt` permission on the CMK to call this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GetSecretValue&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetSecretValue|The operation that you want to perform. Set the value to GetSecretValue. |
|SecretName|String|Yes|secret001|The name of the secret whose value you want to obtain. |
|VersionStage|String|No|ACSCurrent|The stage label that marks the secret version. If you specify this parameter, Secrets Manager returns the secret value of the version that is marked with the specified stage label.

 Default value: **ACSCurrent** |
|VersionId|String|No|00000000000000000000000000000001|The version number of the secret value. If you specify this parameter, Secrets Manager returns the secret value of the specified version. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CreateTime|String|2020-02-21T15:39:26Z|The time when the secret version was created. |
|RequestId|String|8dde04f4-0d27-431c-a0f2-a89c8af016c6|The ID of the request. |
|SecretData|String|testdata1|The secret value. Secrets Manager decrypts the stored secret value in ciphertext and returns it. |
|SecretDataType|String|text|The type of the secret value.

 Valid values:

 -   **binary**
-   **text** |
|SecretName|String|secret001|The name of the secret. |
|VersionId|String|00000000000000000000000000000001|The version number of the secret value. |
|VersionStages|List|\{ "VersionStage": \[ "ACSCurrent" \] \}|Stage labels that mark the secret version. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetSecretValue
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretName>secret001</SecretName>
<VersionId>00000000000000000000000000000001</VersionId>
<SecretData>testdata1</SecretData>
<SecretDataType>text</SecretDataType>
<VersionStages>
    <VersionStage>ACSCurrent</VersionStage>
</VersionStages>
<CreateTime>2020-02-21T15:39:26Z</CreateTime>
<RequestId>8dde04f4-0d27-431c-a0f2-a89c8af016c6</RequestId>
```

`JSON` format

```
{
    "SecretName": "secret001",
    "VersionId": "00000000000000000000000000000001",
    "SecretData": "testdata1",
    "SecretDataType": "text",
    "VersionStages": {
        "VersionStage": [
            "ACSCurrent"
        ]
    },
    "CreateTime": "2020-02-21T15:39:26Z",
    "RequestId": "8dde04f4-0d27-431c-a0f2-a89c8af016c6"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

