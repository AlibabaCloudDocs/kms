# EnableKey

Enables a customer master key \(CMK\) to encrypt and decrypt data.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=EnableKey&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|EnableKey|The operation that you want to perform. Set the value to EnableKey. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID of the CMK. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|efb1cbbd-a093-4278-bc03-639dd4fcc207|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=EnableKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
      <RequestId>efb1cbbd-a093-4278-bc03-639dd4fcc207</RequestId>
</KMS>
```

`JSON` format

```
{
"RequestId": "efb1cbbd-a093-4278-bc03-639dd4fcc207"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

