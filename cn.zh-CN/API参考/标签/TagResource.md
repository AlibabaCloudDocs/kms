# TagResource

调用TagResource接口为主密钥、凭据或证书绑定标签。

使用限制：您最多可以为主密钥、凭据或证书分别绑定10个标签。

本文将提供一个示例，为ID为`08c33a6f-4e0a-4a1b-a3fa-7ddf****`的密钥绑定标签`[{\"TagKey\":\"S1key1\",\"TagValue\":\"S1val1\"},{\"TagKey\":\"S1key2\",\"TagValue\":\"S2val2\"}]`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=TagResource&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|TagResource|要执行的操作，取值：TagResource。 |
|Tags|String|是|\[\{\\"TagKey\\":\\"S1key1\\",\\"TagValue\\":\\"S1val1\\"\},\{\\"TagKey\\":\\"S1key2\\",\\"TagValue\\":\\"S2val2\\"\}\]|一个或多个标签。格式为Tag对象数组。

 Tag对象属性如下：

 -   TagKey：标签键。
-   TagValue：标签值。 |
|KeyId|String|否|08c33a6f-4e0a-4a1b-a3fa-7ddf\*\*\*\*|密钥ID。主密钥（CMK）的全局唯一标识符。

 **说明：** KeyId、SecretName和CertificateId必须且只能指定其中一个参数。 |
|SecretName|String|否|MyDbC\*\*\*\*|凭据名称。

 **说明：** KeyId、SecretName和CertificateId必须且只能指定其中一个参数。 |
|CertificateId|String|否|770dbe42-e146-43d1-a55a-1355db86\*\*\*\*|证书ID。

 **说明：** KeyId、SecretName和CertificateId必须且只能指定其中一个参数。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=TagResource
&KeyId=08c33a6f-4e0a-4a1b-a3fa-7ddf****
&Tags=[{\"TagKey\":\"S1key1\",\"TagValue\":\"S1val1\"},{\"TagKey\":\"S1key2\",\"TagValue\":\"S2val2\"}]
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
    <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

`JSON`格式

```
{
    "RequestId":"4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

