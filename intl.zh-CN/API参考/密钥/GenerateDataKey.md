# GenerateDataKey

调用GenerateDataKey接口生成一个随机的数据密钥，用于本地数据加密。

API随机生成的数据密钥通过您指定的主密钥（CMK）加密后，返回数据密钥的密文和明文。您可以使用返回的数据密钥明文，在KMS之外对数据进行本地离线加密。在存储加密后的数据时，也需要存储数据密钥的密文。您可以通过响应中的Plaintext字段获取到数据密钥的明文，通过CiphertextBlob字段获取到数据密钥的密文。

在请求中指定的CMK，仅会被用作数据密钥的加密，和数据密钥的生成无关。KMS不会记录或存储随机生成的数据密钥，您需要负责对数据密钥（密文）进行持久化。

建议您使用以下方式在本地进行数据加密：

-   调用GenerateDataKey接口，获得数据加密密钥。
-   使用数据密钥的明文（通过响应中的Plaintext字段返回），在本地完成离线数据加密，随后清除内存中的数据密钥明文。
-   将数据密钥的密文（通过响应中的CiphertextBlob字段返回），和本地离线加密后的数据一并进行存储。

在本地解密数据：

-   调用[Decrypt](~~28950~~)接口解密本地存储的数据密钥的密文。这一操作将返回数据密钥的明文。
-   使用数据密钥的明文，在本地完成离线数据解密，随后清除内存中的数据密钥明文。

本文将提供一个示例，为ID为`1234abcd-12ab-34cd-56ef-12345678****`的密钥生成随机的数据密钥。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=GenerateDataKey&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GenerateDataKey|要执行的操作，取值：GenerateDataKey。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|主密钥（CMK）的全局唯一标识符。

 该参数也可以被指定为主密钥绑定的别名，详情请参见[别名使用说明](~~68522~~)。 |
|KeySpec|String|否|AES\_256|指定生成的数据密钥的长度，取值：

 -   AES\_256：256比特的对称密钥。
-   AES\_128：128比特的对称密钥。

 **说明：** 建议使用KeySpec或者NumberOfBytes来指定数据密钥长度。如果两者都不指定，KMS生成256比特的数据密钥；如果两者都被指定，KMS会忽略KeySpec参数。 |
|NumberOfBytes|Integer|否|256|指定生成的数据密钥的长度。

 取值：1~1024。

 单位：字节。 |
|EncryptionContext|Json|否|\{"Example":"Example"\}|key/value对的JSON字符串。如果指定了该参数，则在调用Decrypt时需要提供同样的参数，详情请参见[EncryptionContext](~~42975~~)。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CiphertextBlob|String|ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS\*\*\*\*|数据密钥被指定CMK的主版本加密后的密文。 |
|KeyId|String|599fa825-17de-417e-9554-bb032cc6\*\*\*\*|主密钥的全局唯一标识符。

 **说明：** 如果请求中的KeyId参数使用的是CMK的别名，在响应中会返回别名对应的CMK标识符。 |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|密钥版本ID。主密钥版本的全局唯一标识符。 |
|Plaintext|String|QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0|数据密钥的明文经过Base64编码的后的值。 |
|RequestId|String|7021b6ec-4be7-4d3c-8a68-1e85d4d515a0|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
          <CiphertextBlob>ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS****</CiphertextBlob>
          <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
          <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
          <Plaintext>QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0</Plaintext>
          <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
```

`JSON`格式

```
{
        "CiphertextBlob": "ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS****",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
        "Plaintext": "QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

