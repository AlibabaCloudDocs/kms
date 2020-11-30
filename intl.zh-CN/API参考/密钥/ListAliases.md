# ListAliases

调用ListAliases接口查询当前用户在当前地域的所有别名。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=ListAliases&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListAliases|要执行的操作，取值：ListAliases。 |
|PageNumber|Integer|否|1|当前页数。

 取值范围：大于0的整数。

 默认值：1。 |
|PageSize|Integer|否|10|每页返回的结果个数。

 取值范围：0~100。

 默认值：10。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Aliases|Array of Alias| |用户别名。 |
|Alias| | | |
|AliasArn|String|acs:kms:cn-hangzhou:123456:alias/ExampleAlias1|别名的ARN。 |
|AliasName|String|alias/ExampleAlias1|别名的唯一标识符。 |
|KeyId|String|08c33a6f-4e0a-4a1b-a3fa-7ddfa1d\*\*\*\*|别名对应的主密钥（CMK）。 |
|PageNumber|Integer|1|当前页数。 |
|PageSize|Integer|10|每页的返回结果个数。 |
|RequestId|String|1b57992c-834b-4811-a889-f8bac1ba0353|请求ID。 |
|TotalCount|Integer|1|返回的别名总数。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListAliases
&PageNumber=1
&PageSize=10
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
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

`JSON` 格式

```
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

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

