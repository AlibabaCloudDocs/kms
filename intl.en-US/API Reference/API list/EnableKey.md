# EnableKey {#concept_35150_zh .concept}

Sets the state of the specified CMK to Enabled, thereby permitting its use for cryptographic operations.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|ID of the request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=EnableKey
&KeyId=<cmkid>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
"RequestId": "efb1cbbd-a093-4278-bc03-639dd4fcc207"
}

```

 `XML`format

```
//xml response

<KMS>
    <RequestId>efb1cbbd-a093-4278-bc03-639dd4fcc207</RequestId>
</KMS>

```

