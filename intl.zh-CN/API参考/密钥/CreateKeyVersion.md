# CreateKeyVersion

调用CreateKeyVersion接口为用户主密钥（CMK）创建密钥版本。

使用限制：

-   您只能为非对称类型的CMK创建密钥版本，且CMK必须处于开启（Enabled）状态。您可以调用[CreateKey](~~28947~~) 接口创建非对称密钥，调用[DescribeKey](~~28952~~) 接口查询密钥状态（KeyState）。
-   创建密钥版本的最小间隔为7天。您可以调用[DescribeKey](~~28952~~) 接口查询上次创建密钥版本的时间（LastRotationDate）。
-   PrivateKeyStore中的CMK不支持创建密钥版本。
-   每个地域最多支持创建50个非对称密钥版本。

本文将提供一个示例，为ID为`0b30658a-ed1a-4922-b8f7-a673ca9c****`的CMK创建密钥版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateKeyVersion&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateKeyVersion|要执行的操作，取值：CreateKeyVersion。 |
|KeyId|String|是|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|用户主密钥（CMK）的全局唯一标识符。

 **说明：** 该参数也可以被指定为CMK绑定的别名。更多信息，请参见[别名概述](~~68522~~)。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyVersion|Struct| |密钥版本的元数据。 |
|CreationDate|String|2019-08-02T10:38:27Z|创建密钥版本的时间（UTC时间）。 |
|KeyId|String|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|用户主密钥（CMK）的全局唯一标识符。 |
|KeyVersionId|String|c0a3d5dc-0b47-4199-a050-b289349a\*\*\*\*|密钥版本的标识符。 |
|RequestId|String|b96f250a-4b75-498c-91be-22c6928f85be|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateKeyVersion
&KeyId=0b30658a-ed1a-4922-b8f7-a673ca9c****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
    <KeyVersion>
        <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c****</KeyId>
        <KeyVersionId>c0a3d5dc-0b47-4199-a050-b289349a****</KeyVersionId>
        <CreationDate>2019-08-02T10:38:27Z</CreationDate>
    </KeyVersion>
    <RequestId>b96f250a-4b75-498c-91be-22c6928f85be</RequestId>
</KMS>
```

`JSON`格式

```
{
        "KeyVersion": {
                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c****",
                "KeyVersionId": "c0a3d5dc-0b47-4199-a050-b289349a****",
                "CreationDate": "2019-08-02T10:38:27Z"
        },
        "RequestId": "b96f250a-4b75-498c-91be-22c6928f85be"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

