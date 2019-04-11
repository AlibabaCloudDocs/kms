# DeleteAlias {#concept_68626_zh .concept}

Deletes the specified alias.

## Request parameters { .section}

|Name|Type|Required|Description|
|AliasName|String|Yes|The alias to be deleted.-   The prefix `alias/` must be included.
-   Excluding the prefix, the minimum length of an alias is 1 and the maximum length is 255.

|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|The ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteAlias
&AliasName=<alias name>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "RequestId": "4c8ae23f-3a42-6791-a      4ba-1faa77831c28"
}

```

 `XML` format

```
//xml response
<KMS>
        <RequestId>4c8ae23f-3a42-6791-a 4ba-1faa77831c28</RequestId>
</KMS>

```

