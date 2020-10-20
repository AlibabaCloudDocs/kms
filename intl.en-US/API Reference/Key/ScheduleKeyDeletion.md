# ScheduleKeyDeletion

Deletes a specified CMK.

During the scheduled deletion time, the CMK is in the PendingDeletion state and cannot be used to encrypt data, decrypt data, or generate data keys.

After a CMK is deleted, it cannot be recovered, and the data and ciphertext data keys encrypted by using this CMK cannot be decrypted. Therefore, to prevent you from deleting CMKs by mistake, KMS allows you to only schedule key deletion tasks. You cannot immediately delete CMKs. If you want to delete a CMK, call the [DisableKey](~~35151~~) operation to disable it.

You must specify a waiting period of 7 to 30 days when you call this operation. The waiting period starts from the time you submit the request. You can call the [CancelKeyDeletion](~~44197~~) operation to cancel the deletion before the waiting period ends.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=ScheduleKeyDeletion&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ScheduleKeyDeletion|The operation that you want to perform. Set the value to ScheduleKeyDeletion. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID of the CMK. |
|PendingWindowInDays|Integer|No|7|The number of days before the CMK is deleted. During this period, the CMK is in the PendingDeletion state. After this period ends, you cannot cancel the deletion.

 Valid values: 7 to 30.

 Unit: days. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3da5b8cc-8107-40ac-a170-793cd181d7b7|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ScheduleKeyDeletion
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
      <RequestId>3da5b8cc-8107-40ac-a170-793cd181d7b7</RequestId>
</KMS>
```

`JSON` format

```
{
"RequestId": "3da5b8cc-8107-40ac-a170-793cd181d7b7"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|Throttling|Request was denied due to request throttling.|The error message returned because your traffic in this period has exceeded the limit. If your business requirements are not met, submit a ticket.|
|404|Forbidden.KeyNotFound|The specified Key is not found.|The error message returned because the specified key does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

