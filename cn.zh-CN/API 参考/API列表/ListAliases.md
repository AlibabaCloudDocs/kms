# ListAliases {#concept_68627_zh .concept}

返回当前用户在当前区域的所有别名。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|PageNumber|Integer|否|当前页数。 参数值为大于 0 的整数，默认为1。|
|PageSize|Integer|否|每页返回的结果个数。参数值为 0 到 101 之间的整数。默认为 10。|

## 返回参数 { .section}

|名称|类型|描述|
|AliasName|String|别名的唯一标识符。|
|AliasArn|String|别名的 ARN。|
|KeyId|String|别名对应的 CMK。|
|TotalCount|Integer|返回的 CMK 总数。|
|PageNumber|Integer|当前页数。|
|PageSize|Integer|每页的返回结果个数。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListAliases
&PageNumber=1
&PageSize=10
&<公共请求参数>
			
```

**返回示例**

`JSON` 格式

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

`XML` 格式

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

