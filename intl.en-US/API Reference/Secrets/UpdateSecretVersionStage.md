# UpdateSecretVersionStage

Updates the stage label that marks a secret version.

You can use this operation to achieve the following purposes:

-   Use a specified stage label to mark a new secret version.
-   Remove a specific stage label from an existing secret version.

Limits: This operation is available only for standard secrets.

In this example, the stage label that marks the version of the `secret001` secret is updated. The stage label `ACSCurrent` is used to mark the `002` version.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateSecretVersionStage&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateSecretVersionStage|The operation that you want to perform. Set the value to UpdateSecretVersionStage. |
|SecretName|String|Yes|secret001|The name of the secret. |
|VersionStage|String|Yes|ACSCurrent|The specified stage label. Valid values:

 -   ACSCurrent
-   ACSPrevious
-   Custom stage label |
|RemoveFromVersion|String|No|001|The version from which you want to remove the specified stage label.

 **Note:** You must specify at least one of the RemoveFromVersion and MoveToVersion parameters. |
|MoveToVersion|String|No|002|The version to which you want to apply the specified stage label.

 **Note:**

-   You must specify at least one of the RemoveFromVersion and MoveToVersion parameters.
-   If the VersionStage parameter is set to ACSCurrent or ACSPrevious, this parameter is required. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|8cad259f-4d77-40ec-bbd7-b9c47a423bb9|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=UpdateSecretVersionStage
&SecretName=secret001
&VersionStage=ACSCurrent
&MoveToVersion=002
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <RequestId>8cad259f-4d77-40ec-bbd7-b9c47a423bb9</RequestId>  
</KMS>
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

