# SetDeletionProtection

Enables or disables deletion protection for a customer master key \(CMK\).

Precautions:

-   After you enable deletion protection for a CMK, you cannot delete the CMK. If you want to delete the CMK, you must first disable deletion protection for the CMK.
-   Before you can call the SetDeletionProtection operation, make sure that the required CMK is not in the Pending Deletion state. You can call the [DescribeKey](~~28952~~) operation to query the CMK status, which is specified by the KeyState parameter.

You can enable deletion protection for the CMK whose Alibaba Cloud Resource Name \(ARN\) is `acs:kms:cn-hangzhou:123213123****:key/0225f411-b21d-46d1-be5b-93931c82****` by using parameter settings provided in this topic. The CMK ARN is specified by the ProtectedResourceArn parameter.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=SetDeletionProtection&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|SetDeletionProtection|The operation that you want to perform. Set the value to SetDeletionProtection. |
|EnableDeletionProtection|Boolean|Yes|true|Specifies whether to enable deletion protection. Valid values:

 -   true: enables deletion protection
-   false: disables deletion protection |
|ProtectedResourceArn|String|Yes|acs:kms:cn-hangzhou:123213123\*\*\*\*:key/0225f411-b21d-46d1-be5b-93931c82\*\*\*\*|The ARN of the CMK for which you want to set deletion protection.

 You can call the [DescribeKey](~~28952~~) operation to query the CMK ARN. |
|DeletionProtectionDescription|String|No|The CMK is being used by XXX. Deletion protection is set.|The description of deletion protection.

 **Note:** This parameter takes effect only when you set the EnableDeletionProtection parameter to true. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=SetDeletionProtection
&EnableDeletionProtection=true
&ProtectedResourceArn=acs:kms:cn-hangzhou:123213123****:key/0225f411-b21d-46d1-be5b-93931c82****
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
    "RequestId":"3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

