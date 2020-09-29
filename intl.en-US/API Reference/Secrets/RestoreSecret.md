# RestoreSecret

Restores a deleted secret.

You can only use this operation to restore a deleted secret that is within its recovery period. If you set **ForceDeleteWithoutRecovery** to **true** when you delete the secret, you cannot restore it.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=RestoreSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RestoreSecret|The operation that you want to perform.

 Set the value to **RestoreSecret**. |
|SecretName|String|Yes|secret001|The name of the secret you want to restore. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|e4885adf-548f-4ca5-8075-f540bbd3a55f|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=RestoreSecret
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<RequestId>e4885adf-548f-4ca5-8075-f540bbd3a55f</RequestId>
<SecretName>secret001</SecretName>
```

`JSON` format

```
{
    "RequestId": "e4885adf-548f-4ca5-8075-f540bbd3a55f",
    "SecretName": "secret001"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

