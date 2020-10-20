# UpdateKeyDescription

Updates the description of a specified CMK.

This operation replaces the description of the CMK \(the Description value in [DescribeKey](~~28952~~)\) with the value that you specify. You can add, modify, or delete the description of the CMK through this operation.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateKeyDescription&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateKeyDescription|The operation that you want to perform. Set the value to UpdateKeyDescription. |
|Description|String|Yes|key description example|The description of the CMK. This description includes the purpose of the CMK, such as the types of data that you want to protect and applications that can use the CMK. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID of the CMK. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateKeyDescription
&Description=key description example
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
   <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` format

```
{
	"RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

