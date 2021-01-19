# CreateKeyVersion

为主密钥创建一个新的密钥版本。

仅适用于非对称类型主密钥，且主密钥必须处于开启（Enabled）状态。创建密钥版本的最小间隔为7天，如果在上次创建密钥版本（通过**LastRotationDate**属性查看）的7天之内调用此接口，将返回错误码**Rejected.UnsupportedOperation**。每个用户在每个地域最多持有50个非对称密钥版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateKeyVersion&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateKeyVersion|系统规定参数。取值：CreateKeyVersion。 |
|KeyId|String|是|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|主密钥（CMK）的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|b96f250a-4b75-498c-91be-22c6928f85be|本次请求的ID。 |
|KeyVersion|Struct| |密钥版本的元数据。 |
|KeyId|String|0b30658a-ed1a-4922-b8f7-a673ca9c\*\*\*\*|主密钥的全局唯一标识符。 |
|KeyVersionId|String|c0a3d5dc-0b47-4199-a050-b289349a\*\*\*\*|密钥版本的标志符。 |
|CreationDate|String|2019-08-02T10:38:27Z|创建密钥版本时的日期和时间（UTC时间）。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=CreateKeyVersion
&KeyId=0b30658a-ed1a-4922-b8f7-a673ca9c****
&<公共请求参数>
```

正常返回示例

`XML` 格式

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

`JSON` 格式

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

