# CancelKeyDeletion {#concept_44197_zh .concept}

Cancels the deletion of a CMK. When this operation is successful, the CMK is set to **Enabled** state.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CancelKeyDeletion
&KeyId=<cmkid>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
"RequestId": "3da5b8cc-8107-40ac-a170-793cd181d7b7"
}

```

 `XML` format

```
//xml response
<KMS>
    <RequestId>3da5b8cc-8107-40ac-a170-793cd181d7b7</RequestId>
</KMS>

```

