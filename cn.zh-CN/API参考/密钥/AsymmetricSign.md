# AsymmetricSign

调用AsymmetricSign接口使用非对称密钥进行签名。

仅支持**Usage**为**SIGN/VERIFY**的非对称密钥。支持的签名算法如下表：

|KeySpec

|Algorithm

|说明 |
|---------|-----------|----|
|RSA\_2048

|RSA\_PSS\_SHA\_256

|RSASSA-PSS using SHA-256 and MGF1 with SHA-256 |
|RSA\_2048

|RSA\_PKCS1\_SHA\_256

|RSASSA-PKCS1-v1\_5 using SHA-256 |
|RSA\_3072

|RSA\_PSS\_SHA\_256

|RSASSA-PSS using SHA-256 and MGF1 with SHA-256 |
|RSA\_3072

|RSA\_PKCS1\_SHA\_256

|RSASSA-PKCS1-v1\_5 using SHA-256 |
|EC\_P256

|ECDSA\_SHA\_256

|ECDSA on the P-256 Curve\(secp256r1\) with a SHA-256 digest |
|EC\_P256K

|ECDSA\_SHA\_256

|ECDSA on the P-256K Curve\(secp256k1\) with a SHA-256 digest |
|EC\_SM2

|SM2DSA

|SM2椭圆曲线数字签名算法 |

**说明：** 按照国家标准GBT32918，计算SM2签名值时，**Digest**参数不是对原始消息直接计算SM3摘要，而是对Z\(A\)和M的拼接值计算的摘要，其中M是待签名的原始消息，Z\(A\)是GBT32918中定义的用户A的杂凑值。

本文将提供一个示例，使用密钥ID为`5c438b18-05be-40ad-b6c2-3be6752c****`、密钥版本ID为`2ab1a983-7072-4bbc-a582-584b5bd8****`的非对称密钥，通过签名算法`RSA_PSS_SHA_256`对摘要信息`ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiuy****=`进行签名。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=AsymmetricSign&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|AsymmetricSign|要执行的操作，取值：AsymmetricSign。 |
|Algorithm|String|是|RSA\_PSS\_SHA\_256|签名算法。 |
|Digest|String|是|ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiu\*\*\*\*=|使用Algorithm中对应的哈希算法，对原始消息生成的摘要。

 **说明：** 使用Base64编码。 |
|KeyId|String|是|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥（CMK）的全局唯一标识符。

 **说明：** 该参数也可以被指定为主密钥绑定的别名。更多信息，请参见[别名使用说明](~~68522~~)。 |
|KeyVersionId|String|是|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|密钥版本ID。密钥版本的全局唯一标识符。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|主密钥的全局唯一标识符。

 **说明：** 如果请求中的KeyId参数使用的是主密钥的别名，在响应中会返回别名对应的主密钥标识符。 |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|密钥版本ID。密钥版本的全局唯一标识符。 |
|Value|String|M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq\*\*\*\*==|计算出来的签名。

 **说明：** 使用Base64编码。 |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=AsymmetricSign
&Algorithm=RSA_PSS_SHA_256
&Digest=ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiu****=
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <Value>M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq****==</Value>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON`格式

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "Value": "M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq****==",
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

