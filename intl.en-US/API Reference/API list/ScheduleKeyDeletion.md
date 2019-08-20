# ScheduleKeyDeletion {#concept_44196_zh .concept}

Schedules the deletion of a CMK.

-   During waiting period, the key is in **PendingDeletion** state and cannot be used for encryption, decryption, or data key generation.
-   A deleted CMK cannot be recovered. The data it encrypted, and the DataKey it generated cannot be decrypted again. Therefore, you must make a request to KMS for deleting a CMK. We recommend that you use [DisableKey](intl.en-US/API Reference/API list/DisableKey.md#) instead if possible.
-   You must specify a waiting period when you make the request. The period must be between 7 and 30 days. You can use [CancelKeyDeletion](intl.en-US/API Reference/API list/CancelKeyDeletion.md#) to cancel the request after submission but before the waiting period ends.
-   The CMK is deleted within 24 hours after the waiting period ends. The API server uses UTC format. For example, a user makes a request at 14:00, Sep 10, 2016. The waiting period is 7 days. KMS deletes the CMK within 24 hours after 14:00, Sep 17.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK.|
|PendingWindowInDays|Integer|Yes|The waiting period, specified in number of days. During this period, you can cancel the CMK in **PendingDeletion** status. After the waiting period expires, you cannot cancel the deletion. The value must be between 7 and 30.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ScheduleKeyDeletion
&KeyId=<your-key-id>
&PendingWindowInDays=[7~30]
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
"RequestId": "52ac67cb-3d3d-4ada-b4e2-7047660d3ce9"
}

```

 `XML` format

```
//xml response
<KMS>
    <RequestId>52ac67cb-3d3d-4ada-b4e2-7047660d3ce9</RequestId>
</KMS>

```

