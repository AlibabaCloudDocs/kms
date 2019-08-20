# UpdateAlias {#concept_68625_zh .concept}

Associates an existing alias with a different CMK.

## Request parameters { .section}

|Name|Type|Required|Description|
|AliasName|String|Yes|The name of the alias to be modified.1.  The prefix `alias/` must be included.
2.  Excluding the prefix, the minimum length of an alias is 1 and the maximum length is 255.

|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateAlias
&AliasName=<alias name>
&KeyId=<target keyid>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "RequestId": "1d2baaf3-d357-46c2-832e-13560c2bd9cd"
}

```

 `XML` format

```
//xml response
<KMS>
        <RequestId>1d2baaf3-d357-46c2-832e-13560c2bd9cd</RequestId>
</KMS>

```

