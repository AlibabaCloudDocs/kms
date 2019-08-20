# ListAliases {#concept_68627_zh .concept}

Gets a list of all aliases in the caller’s account and region.

## Request parameters { .section}

|Name|Type|Required|Description|
|PageNumber|Integer|No|The current page number. Valid value: an integer greater than 0. The default value is 1.|
|PageSize|Integer|No|The number of items on each page. Valid value: an integer between 0 and 101. The default value is 10.The default is 10.|

## Response parameters { .section}

|Name|Type|Description|
|AliasName|String|The unique identifier of an alias.|
|AliasArn|String|The ARN of the alias.|
|KeyId|String|The CMK associated with an alias.|
|TotalCount|Integer|The total number of items returned.|
|PageNumber|Integer|The current page number.|
|PageSize|Integer|The number of items on each page.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListAliases
&PageNumber=1
&PageSize=10
&<Common Request Parameters>
			
```

**Response example**

`JSON` format

```
//json response
{
        "Aliases": {
                "Alias": [
                        {
                                "AliasName": "alias/ExampleAlias1",
                                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d****",
                                "AliasArn": "acs:kms:cn-hangzhou:123456:alias/ExampleAlias1"
                        }
        ]
        },
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 10,
        "RequestId": "1b57992c-834b-4811-a889-f8bac1ba0353"
}
			
```

`XML` format

```
//xml response
<KMS>
        <Aliases>
                <Alias>
                        <AliasName>alias/ExampleAlias1</AliasName>
                        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1****</KeyId>
                        <AliasArn>acs:kms:cn-hangzhou:123456:alias/ExampleAlias1</AliasArn>
                </Alias>
        </Aliases>
        <TotalCount>1</TotalCount>
        <PageNumber>1</PageNumber>
        <PageSize>10</PageSize>
        <RequestId>1b57992c-834b-4811-a889-f8bac1ba0353</RequestId>
</KMS>
			
```

