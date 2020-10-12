# DeleteAlias

Deletes an alias.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DeleteAlias&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteAlias|The operation that you want to perform. Set the value to DeleteAlias. |
|AliasName|String|Yes|alias/example|The alias that you want to delete.

 The value must be 1 to 255 characters in length and must include the alias/ prefix. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4c8ae23f-3a42-6791-a4ba-1faa77831c28|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteAlias
&AliasName=alias/example
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
          <RequestId>4c8ae23f-3a42-6791-a4ba-1faa77831c28</RequestId>
</KMS>
```

`JSON` format

```
{
        "RequestId": "4c8ae23f-3a42-6791-a4ba-1faa77831c28"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

