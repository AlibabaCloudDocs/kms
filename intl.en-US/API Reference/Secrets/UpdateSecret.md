# UpdateSecret

Updates the metadata of a secret.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateSecret|The operation that you want to perform. Set the value to UpdateSecret. |
|SecretName|String|Yes|secret001|The name of the secret whose metadata you want to update. |
|Description|String|No|datainfo|The description of the updated secret. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=UpdateSecret
&Description=datainfo
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretName>secret001</SecretName>
<RequestId>5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47</RequestId>
```

`JSON` format

```
{
    "SecretName":"secret001",  
    "RequestId": "5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

