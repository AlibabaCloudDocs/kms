# UntagResource

Deletes tags from a customer master key \(CMK\) or secret.

You must specify either KeyId or SecretName.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UntagResource&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UntagResource|The operation that you want to perform. Set the value to UntagResource. |
|TagKeys|String|Yes|\["tagkey1","tagkey2"\]|One or more tag keys. Multiple tag keys are separated by commas \(,\).

 You need to specify only the tag keys, not the tag values.

 Each tag key must be 1 to 128 bytes in length. |
|KeyId|String|No|08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|The globally unique ID of the CMK.

 **Note:** Set either this parameter or SecretName. |
|SecretName|String|No|MyDbC\*\*\*\*|The name of the secret.

 **Note:** Set either this parameter or KeyId. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UntagResource
&KeyId=08c33a6f-4e0a-4a1b-a3fa-7ddf****
&TagKeys=["tagkey1","tagkey2"]
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

`JSON` format

```
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

