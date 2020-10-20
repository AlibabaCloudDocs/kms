# DeleteKeyMaterial

Deletes the key material that you imported.

This operation does not delete the CMK that is created by using the key material.

If the CMK is in the PendingDeletion state, the state of the CMK and the scheduled deletion time do not change after you call this operation. If the CMK is not in the PendingDeletion state, the state of the CMK changes to PendingImport after you call this operation.

After you delete the key material, you can upload only the same key material into the CMK.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DeleteKeyMaterial&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteKeyMaterial|The operation that you want to perform. Set the value to DeleteKeyMaterial. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID of the CMK. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteKeyMaterial
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
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

