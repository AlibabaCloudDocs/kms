# ListSecrets

调用ListSecrets接口查询当前用户在当前地域创建的所有凭据。

此接口返回凭据对象的元数据信息，不返回被加密存储的凭据值。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=ListSecrets&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ListSecrets|要执行的操作，取值：ListSecrets。 |
|FetchTags|String|否|false|返回值中是否包含凭据的资源标签。取值：

 -   true：包含。
-   false（默认值）：不包含。 |
|PageNumber|Integer|否|1|当前页数。

 取值范围：大于0。

 默认值：1。 |
|PageSize|Integer|否|10|每页返回值的个数。

 取值范围：1~100。

 默认值：10。 |
|Filters|String|否|\[\{"Key":"SecretName", "Values":\["$Val1","$Val2"\]\}\]|凭据过滤器。由Key-Values键值对组成，长度为0~1。

 -   Key
    -   描述：需要过滤的属性。
    -   类型：String。
    -   取值：
        -   SecretName：凭据名称。
        -   Description：凭据描述。
        -   TagKey：标签键。
        -   TagValue：标签值。
-   Values
    -   描述：期望过滤后包含的值。
    -   类型：String。
    -   长度：0~10。
    -   取值说明：
        -   Key取值为SecretName时：长度为1~192个字符，可包含英文字母、数字和特殊字符 `_/+=.@-`。
        -   Key取值为Description时：长度为1~256个字符。
        -   Key取值为TagKey时：长度为1~256个字符，可包含英文字母、数字和特殊字符`/_-.+=@:`。
        -   Key取值为TagValue时：长度为1~256个字符，可包含英文字母、数字和特殊字符 `/_-.+=@:`。

 Filters同一个Key中的多个Value之间的逻辑关系为OR。例如：输入`[ {"Key":"SecretName", "Values":["sec1","sec2"]} ]`时，语义为： `(SecretName=sec1 OR SecretName=sec2)`。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|PageNumber|Integer|1|当前页数。 |
|PageSize|Integer|10|每页返回值的个数。 |
|RequestId|String|e8818e65-5c5b-4a0e-a571-8f50b59920a7|请求ID。 |
|SecretList|Array of Secret| |凭据列表。 |
|Secret| | | |
|CreateTime|String|2020-02-21T01:24:45Z|创建时间。 |
|PlannedDeleteTime|String|2020-03-21T01:24:45Z|计划删除时间。 |
|SecretName|String|secret001|凭据名称。 |
|Tags|Array of Tag| |凭据的资源标签。如果请求中未指定获取资源标签，则不包含此参数。 |
|Tag| | | |
|TagKey|String|key1|标签键。 |
|TagValue|String|val1|标签值。 |
|UpdateTime|String|2020-02-21T15:22:45Z|更新时间。 |
|TotalCount|Integer|20|凭据列表中的凭据个数。 |

## 示例

请求示例

```
ttps://kms.cn-hangzhou.aliyuncs.com/?Action=ListSecrets
&PageNumber=1
&PageSize=10
&Filters=[{"Key":"SecretName", "Values":["$Val1","$Val2"]}]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<SecretList>
    <Secret>
        <SecretName>secret001</SecretName>
        <CreateTime>2020-02-21T01:24:45Z</CreateTime>
        <UpdateTime>2020-02-21T01:24:45Z</UpdateTime>
        <Tags>
        </Tags>
    </Secret>
    <Secret>
        <SecretName>secret004</SecretName>
        <CreateTime>2020-02-21T15:22:45Z</CreateTime>
        <UpdateTime>2020-02-21T15:22:45Z</UpdateTime>
        <Tags>
            <Tag>
                <TagKey>key1</TagKey>
                <TagValue>val1</TagValue>
            </Tag>
            <Tag>
                <TagKey>key2</TagKey>
                <TagValue>val2</TagValue>
            </Tag>
        </Tags>
    </Secret>
</SecretList>
<RequestId>edbdc10d-3bcb-4690-95cb-3bf5664e1f02</RequestId>
<PageNumber>1</PageNumber>
<PageSize>10</PageSize>
<TotalCount>2</TotalCount>
```

`JSON` 格式

```
{
	"SecretList": {
		"Secret": [
			{
				"SecretName": "secret001",
				"CreateTime": "2020-02-21T01:24:45Z",
				"UpdateTime": "2020-02-21T01:24:45Z",
				"Tags": {
					"Tag": []
				}
			},
			{
				"SecretName": "secret004",
				"CreateTime": "2020-02-21T15:22:45Z",
				"UpdateTime": "2020-02-21T15:22:45Z",
				"Tags": {
					"Tag": [
						{
							"TagKey": "key1",
							"TagValue": "val1"
						},
						{
							"TagKey": "key2",
							"TagValue": "val2"
						}
					]
				}
			}
		]
	},
	"RequestId": "edbdc10d-3bcb-4690-95cb-3bf5664e1f02",
	"PageNumber": 1,
	"PageSize": 10,
	"TotalCount": 2
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

