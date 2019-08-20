# DisableKey {#concept_35151_zh .concept}

Sets the state of a CMK to Disabled. The ciphertext encrypted using the CMK cannot be decrypted until the CMK is enabled again.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DisableKey
&KeyId=<cmkid>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
"RequestId": "2fe70ce2-3303-4fd6-b3ac-472fb2705c62"
}

```

 `XML`format

```
//xml response
<KMS>
    <RequestId>2fe70ce2-3303-4fd6-b3ac-472fb2705c62</RequestId>
</KMS>

```

