# CreateAlias {#concept_68624_zh .concept}

Creates an alias for a CMK.

**Note:** 

-   Each CMK can have multiple aliases, but each alias points to only one CMK.
-   The alias name must be unique in one account and region.
-   You can use [UpdateAlias](reseller.en-US/API Reference/API list/UpdateAlias.md#) to update the mapping between the alias and the key.

## Request parameters { .section}

|Name|Type|Required|Description|
|AliasName|String|Yes|- The display name of the key. You can use the alias to call APIs such as `Encrypt`, `GenerateDataKey`, and `DescribeKey`. - Not including the prefix, the minimum length of an alias is 1 and the maximum length is 255. - The prefix `alias/` must be included.|
|KeyId|String|Yes|Globally unique identifier of the CMK.|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|ID of the request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreareAlias
&KeyId=<cmkid>
&AliasName=<alias/example>
&<Common Request Parameters>

```

**Response example**

`JSON` format

```
//json response
{
    "RequestId": "53790170-1096-4ed2-9c3a-244d75c8740a"
}

```

 `XML` format

```
//xml response
<KMS>
    <RequestId>53790170-1096-4ed2-9c3a-244d75c8740a</RequestId>
</KMS>

```

