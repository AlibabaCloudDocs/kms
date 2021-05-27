# AsymmetricEncrypt

调用AsymmetricEncrypt接口使用非对称密钥进行加密。

仅支持**Usage**为**ENCRYPT/DECRYPT**的非对称密钥。支持的加密算法如下表：

|KeySpec

|Algorithm

|说明

|可加密的最大字节数 |
|---------|-----------|----|-----------|
|RSA\_2048

|RSAES\_OAEP\_SHA\_256

|RSAES-OAEP using SHA-256 and MGF1 with SHA-256

|190 |
|RSA\_2048

|RSAES\_OAEP\_SHA\_1

|RSAES-OAEP using SHA1 and MGF1 with SHA1

|214 |
|RSA\_3072

|RSAES\_OAEP\_SHA\_256

|RSAES-OAEP using SHA-256 and MGF1 with SHA-256

|318 |
|RSA\_3072

|RSAES\_OAEP\_SHA\_1

|RSAES-OAEP using SHA1 and MGF1 with SHA1

|342 |
|EC\_SM2

|SM2PKE

|SM2椭圆曲线公钥加密算法

|6047

| |

本文将提供一个示例，使用密钥ID为`5c438b18-05be-40ad-b6c2-3be6752c****`、密钥版本ID为`2ab1a983-7072-4bbc-a582-584b5bd8****`的非对称密钥，通过加密算法`RSAES_OAEP_SHA_1`对明文`SGVsbG8gd29ybGQ=`进行加密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=AsymmetricEncrypt&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AsymmetricEncrypt|要执行的操作，取值：AsymmetricEncrypt。 |
|Algorithm|String|是|RSAES\_OAEP\_SHA\_1|加密算法。 |
|KeyId|String|是|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥（CMK）的全局唯一标识符。

 **说明：** 该参数也可以被指定为主密钥绑定的别名。更多信息，请参加见[别名使用说明](~~68522~~)。 |
|KeyVersionId|String|是|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|密钥版本ID。密钥版本的全局唯一标识符。 |
|Plaintext|String|是|SGVsbG8gd29ybGQ=|要加密的明文，使用Base64编码。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥的全局唯一标识符。

 **说明：** 如果请求中的KeyId参数使用的是主密钥的别名，在响应中会返回别名对应的主密钥标识符。 |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|对明文数据进行加密的主密钥版本号。 |
|CiphertextBlob|String|BQKP+1zK6+ZEMxTP5qaVzcsgXtWplYBKm0NXdSnB5FzliFxE1bSiu4dnEIlca2JpeH7yz1/S6fed630H+hIH6DoM25fTLNcKj+mFB0Xnh9m2+HN59Mn4qyTfcUeadnfCXSWcGBouhXFwcdd2rJ3n337bzTf4jm659gZu3L0i6PLuxM9p7mqdwO0cKJPfGVfhnfMz+f4alMg79WB/NNyE2lyX7/qxvV49ObNrrJbKSFiz8Djocaf0IESNLMbfYI5bXjWkJlX92DQbKhibtQW8ZOJ//ZC6t0AWcUoKL6QDm/dg5koQalcleRinpB+QadFm894sLbVZ9+N4GVsv1Wbjwg==|加密后的密文。

 **说明：** 使用Base64编码。 |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|请求ID。 |

## 示例

请求示例

```
https://[Endpoint]/?Action=AsymmetricEncrypt
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&Algorithm=RSAES_OAEP_SHA_1
&Plaintext=SGVsbG8gd29ybGQ=
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <CiphertextBlob>RKF5WeXJtusIrvuPOjpkA/55EKzi8Wmc/eJ2fQUKphvL750jtInSX1wijw/7jGxUaTHTW6tgIJl2ReN1aI1/wxqGxdzScwsMHxCBncnzQsZF+Fi4UFpI9pr4A1wc2u5Ngwyx9uA4K/kJ5bkS4NvmanxssAPZfSfbJSrAWlCP11tS0Cd54tQVGj4XK9tP9bJDKzKis1NClsOXZtNPX88kUqr3LkgFCsD07IwiePAfI2tn2fzeisje1Q7/d6VkF48c3ZE0DAmnLRujt3yRRGDaKUkI6SUDjuKD4yqBUX15/DKfJtya+JIPQGiO2IEPlhL7+NMT17U0tKtK5ZPNEwxfZw==</CiphertextBlob>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON`格式

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "CiphertextBlob": "RKF5WeXJtusIrvuPOjpkA/55EKzi8Wmc/eJ2fQUKphvL750jtInSX1wijw/7jGxUaTHTW6tgIJl2ReN1aI1/wxqGxdzScwsMHxCBncnzQsZF+Fi4UFpI9pr4A1wc2u5Ngwyx9uA4K/kJ5bkS4NvmanxssAPZfSfbJSrAWlCP11tS0Cd54tQVGj4XK9tP9bJDKzKis1NClsOXZtNPX88kUqr3LkgFCsD07IwiePAfI2tn2fzeisje1Q7/d6VkF48c3ZE0DAmnLRujt3yRRGDaKUkI6SUDjuKD4yqBUX15/DKfJtya+JIPQGiO2IEPlhL7+NMT17U0tKtK5ZPNEwxfZw==",
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

