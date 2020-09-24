# UpdateAlias

调用UpdateAlias接口更新已存在的别名所代表的主密钥（CMK）ID。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateAlias&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateAlias|要执行的操作，取值：UpdateAlias。 |
|AliasName|String|是|alias/example|要操作的别名。

 长度为1~255个字符，必须包含前缀alias/。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|新的密钥ID。主密钥的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|1d2baaf3-d357-46c2-832e-13560c2bd9cd|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateAlias
&AliasName=alias/example
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
          <RequestId>1d2baaf3-d357-46c2-832e-13560c2bd9cd</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "RequestId": "1d2baaf3-d357-46c2-832e-13560c2bd9cd"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|Throttling|Request was denied due to request throttling.|您这个时段的流量已经超限。如果不能满足现有业务要求可以提工单进行申请。|
|404|Forbidden.KeyNotFound|The specified Key is not found.|指定的密钥不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

