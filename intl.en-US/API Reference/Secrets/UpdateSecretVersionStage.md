# UpdateSecretVersionStage

Updates the stage label that marks a secret version.

You can use this operation to achieve the following purposes:

-   Use a specified stage label to mark a new secret version.
-   Remove a specific stage label from an existing secret version.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateSecretVersionStage&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateSecretVersionStage|The operation that you want to perform. Set the value to UpdateSecretVersionStage. |
|SecretName|String|Yes|secret001|The name of the secret whose stage label you want to update. |
|VersionStage|String|Yes|ACSCurrent|The stage label you want to update. |
|RemoveFromVersion|String|No|00000000000000000000000000000001|The version from which you want to remove the specified stage label. |
|MoveToVersion|String|No|00000000000000000000000000000002|The version to which you want to apply the specified stage label. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8cad259f-4d77-40ec-bbd7-b9c47a423bb9|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=UpdateSecretVersionStage
&SecretName=secret001
&VersionStage=ACSCurrent
&MoveToVersion=vid0001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretName>secret001</SecretName>
<RequestId>8cad259f-4d77-40ec-bbd7-b9c47a423bb9</RequestId>
```

`JSON` format

```
{
    "SecretName": "secret001",
    "RequestId": "8cad259f-4d77-40ec-bbd7-b9c47a423bb9"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

