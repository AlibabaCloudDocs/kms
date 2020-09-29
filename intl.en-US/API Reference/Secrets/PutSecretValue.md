# PutSecretValue

Stores the secret value of a new version into a secret object.

This operation is used to store secret values of new versions. It cannot be used to modify the secret value of an existing version.

If you do not specify VersionStage, the newly stored secret value is marked with **ACSCurrent**, and the original version marked with **ACSCurrent** is marked with **ACSPrevious**. If you specify **VersionStage**, the newly stored secret value is marked with the specified stage label.

You must specify a version number. Secrets Manager performs operations based on the following rules:

-   If the specified version number does not exist in the secret object, Secrets Manager creates the new version and stores the secret value.
-   If the specified version number already exists in the secret object and the secret value that matches this existing version is the same as the secret value that you specified, Secrets Manager ignores the request and returns a success message. The request is idempotent.
-   If the specified version number already exists in the secret object but the secret value that matches this existing version is different from the secret value that you specified, Secrets Manager rejects the request and returns a failure message.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=PutSecretValue&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|PutSecretValue|The operation that you want to perform.

 Set the value to **PutSecretValue**. |
|SecretData|String|Yes|importantdata|The secret value that you want to store. It is encrypted and then stored in a specified new version. |
|SecretName|String|Yes|secret001|The name of the secret whose value you want to store. |
|VersionId|String|Yes|00000000000000000000000000000000203|The version number of the secret value you want to store. It must be unique in the secret object. |
|SecretDataType|String|No|text|The type of the secret value that you want to store. Valid values:

 -   **text**
-   **binary**

Default value: **text** |
|VersionStages|String|No|\["ACSCurrent", "UStage1","Ustage2"\]|The stage labels that mark the new secret version. If you do not specify this parameter, Secrets Manager marks it with **ACSCurrent**. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|6d394629-3ae3-4412-bb83-ae95ceb2b5da|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |
|VersionId|String|00000000000000000000000000000000203|The version number of the secret value. |
|VersionStages|List|\{ "VersionStage": \[ "ACSCurrent", "UStage1", "Ustage2" \] \}|Stage labels that mark the version. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=PutSecretValue
&SecretData=importantdata
&SecretDataType=text
&SecretName=secret001
&VersionId=00000000000000000000000000000000203
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretName>secret001</SecretName>
<VersionId>00000000000000000000000000000000203</VersionId>
<VersionStages>
    <VersionStage>ACSCurrent</VersionStage>
    <VersionStage>UStage1</VersionStage>
    <VersionStage>Ustage2</VersionStage>
</VersionStages>
<RequestId>6d394629-3ae3-4412-bb83-ae95ceb2b5da</RequestId>
```

`JSON` format

```
{
    "SecretName": "secret001",
    "VersionId": "00000000000000000000000000000000203",
    "VersionStages": {
        "VersionStage": [
            "ACSCurrent",
            "UStage1",
            "Ustage2"
        ]
    },
    "RequestId": "6d394629-3ae3-4412-bb83-ae95ceb2b5da"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

