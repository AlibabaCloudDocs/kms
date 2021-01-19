# AsymmetricDecrypt

调用AsymmetricDecrypt接口使用非对称密钥进行解密。

仅支持**Usage**为**ENCRYPT/DECRYPT**的非对称密钥。支持的加密算法如下表：

|KeySpec

|Algorithm

|说明

|密文长度（字节） |
|---------|-----------|----|----------|
|RSA\_2048

|RSAES\_OAEP\_SHA\_256

|RSAES-OAEP using SHA-256 and MGF1 with SHA-256

|256 |
|RSA\_2048

|RSAES\_OAEP\_SHA\_1

|RSAES-OAEP using SHA1 and MGF1 with SHA1

|256 |
|EC\_SM2

|SM2PKE

|SM2椭圆曲线公钥加密算法

|最大6144 |

密文可以是**AsymmetricEncrypt** API生成的，也可以是用户侧通过以上加密算法生成的。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=AsymmetricDecrypt&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AsymmetricDecrypt|要执行的操作，取值：**AsymmetricDecrypt**。 |
|Algorithm|String|是|RSAES\_OAEP\_SHA\_1|解密算法。 |
|CiphertextBlob|String|是|BQKP+1zK6+ZEMxTP5qaVzcsgXtWplYBKm0NXdSnB5FzliFxE1bSiu4dnEIlca2JpeH7yz1/S6fed630H+hIH6DoM25fTLNcKj+mFB0Xnh9m2+HN59Mn4qyTfcUeadnfCXSWcGBouhXFwcdd2rJ3n337bzTf4jm659gZu3L0i6PLuxM9p7mqdwO0cKJPfGVfhnfMz+f4alMg79WB/NNyE2lyX7/qxvV49ObNrrJbKSFiz8Djocaf0IESNLMbfYI5bXjWkJlX92DQbKhibtQW8ZOJ//ZC6t0AWcUoKL6QDm/dg5koQalcleRinpB+QadFm894sLbVZ9+N4GVsv1Wbjwg==|解密密文。

 **说明：** 使用Base64编码。 |
|KeyId|String|是|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥（CMK）的全局唯一标识符。

 **说明：** 该参数也可以被指定为CMK绑定的别名，详情请参见[别名使用说明](~~68522~~)。 |
|KeyVersionId|String|是|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|密钥版本的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥的全局唯一标识符。

 **说明：** 如果请求中的KeyId参数使用的是主密钥的别名，在响应中会返回别名对应的主密钥标志符。 |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|对明文数据进行加密的主密钥版本号。 |
|Plaintext|String|SGVsbG8gd29ybGQ=|解密后的明文，使用Base64编码。 |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|请求ID。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=AsymmetricDecrypt
&Algorithm=RSAES_OAEP_SHA_1
&CiphertextBlob=BQKP+1zK6+ZEMxTP5qaVzcsgXtWplYBKm0NXdSnB5FzliFxE1bSiu4dnEIlca2JpeH7yz1/S6fed630H+hIH6DoM25fTLNcKj+mFB0Xnh9m2+HN59Mn4qyTfcUeadnfCXSWcGBouhXFwcdd2rJ3n337bzTf4jm659gZu3L0i6PLuxM9p7mqdwO0cKJPfGVfhnfMz+f4alMg79WB/NNyE2lyX7/qxvV49ObNrrJbKSFiz8Djocaf0IESNLMbfYI5bXjWkJlX92DQbKhibtQW8ZOJ//ZC6t0AWcUoKL6QDm/dg5koQalcleRinpB+QadFm894sLbVZ9+N4GVsv1Wbjwg==
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <Plaintext>SGVsbG8gd29ybGQ=</Plaintext>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON` 格式

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "Plaintext": "SGVsbG8gd29ybGQ=",
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

