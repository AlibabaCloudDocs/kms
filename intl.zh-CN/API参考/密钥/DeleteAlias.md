# DeleteAlias

调用DeleteAlias接口删除别名。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DeleteAlias&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteAlias|要执行的操作，取值：DeleteAlias。 |
|AliasName|String|是|alias/example|要操作的别名。

 长度为1~255个字符，必须包含前缀alias/。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4c8ae23f-3a42-6791-a4ba-1faa77831c28|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteAlias
&AliasName=alias/example
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
          <RequestId>4c8ae23f-3a42-6791-a4ba-1faa77831c28</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "RequestId": "4c8ae23f-3a42-6791-a4ba-1faa77831c28"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

