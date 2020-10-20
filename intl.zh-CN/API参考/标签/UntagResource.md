# UntagResource

调用UntagResource接口删除用户主密钥或凭据的指定标签。

请求中至少指定KeyId或者SecretName其中一个参数，以确定删除的对象。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UntagResource&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UntagResource|要执行的操作，取值：UntagResource。 |
|TagKeys|String|是|\["tagkey1","tagkey2"\]|一个或多个标签键，多个标签键用半角逗号（,）间隔。

 您只需指定标签键，不需要指定标签值。

 长度为1~128个字节。 |
|KeyId|String|否|08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|密钥ID。主密钥（CMK）的全局唯一标识符。

 **说明：** 与参数SecretName只能设置其中一个。 |
|SecretName|String|否|MyDbC\*\*\*\*|凭据名称。

 **说明：** 与参数KeyId只能设置其中一个。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UntagResource
&KeyId=08c33a6f-4e0a-4a1b-a3fa-7ddf****
&TagKeys=["tagkey1","tagkey2"]
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
    <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

`JSON` 格式

```
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

