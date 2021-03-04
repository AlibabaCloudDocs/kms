# UpdateSecret

Updates the metadata of a secret.

In this example, the metadata of the `secret001` secret is updated. The `Description` parameter is set to `datainfo`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateSecret|The operation that you want to perform. Set the value to UpdateSecret. |
|SecretName|String|Yes|secret001|The name of the secret. |
|Description|String|No|datainfo|The description of the secret. |
|ExtendedConfig.CustomData|Json|No|\{"DBName":"app1","Port":"3306"\}|The custom data in the extended configuration of the secret.

 **Note:**

-   If this parameter is specified, the existing extended configuration of the secret is updated.
-   This parameter is unavailable for standard secrets. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=UpdateSecret
&Description=datainfo
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <RequestId>5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47</RequestId>
</KMS>
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

