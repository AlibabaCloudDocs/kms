# CertificatePrivateKeyDecrypt

调用CertificatePrivateKeyDecrypt接口使用指定证书解密数据。

使用限制：请求参数中加密算法需要跟密钥类型对应。

加密算法和密钥类型对照表如下：

|Algorithm

|Key Spec |
|-----------|----------|
|RSAES\_OAEP\_SHA\_1

|RSA\_2048 |
|RSAES\_OAEP\_SHA\_256

|RSA\_2048 |
|SM2PKE

|EC\_SM2 |

本文将提供一个示例，使用ID为`12345678-1234-1234-1234-12345678****`的证书，通过`RSAES_OAEP_SHA_256`加密算法对数据`ZOyIygCyaOW6Gj****MlNKiuyjfzw=`进行解密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CertificatePrivateKeyDecrypt&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CertificatePrivateKeyDecrypt|要执行的操作，取值：CertificatePrivateKeyDecrypt。 |
|Algorithm|String|是|RSAES\_OAEP\_SHA\_256|加密算法，取值：

 -   RSAES\_OAEP\_SHA\_1
-   RSAES\_OAEP\_SHA\_256
-   SM2PKE

**说明：** SM2PKE加密算法仅在中国内地使用托管密码机的地域支持。更多信息，请参见[托管密码机概述](~~125803~~)。 |
|CertificateId|String|是|12345678-1234-1234-1234-12345678\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|CiphertextBlob|String|是|ZOyIygCyaOW6Gj\*\*\*\*MlNKiuyjfzw=|待解密数据。

 使用Base64编码。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CertificateId|String|12345678-1234-1234-1234-12345678\*\*\*\*|证书ID。 |
|Plaintext|String|VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4|解密后的数据。

 使用Base64编码。 |
|RequestId|String|5979d897-d69f-4fc9-87dd-f3bb73c40b80|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CertificatePrivateKeyDecrypt
&Algorithm=RSAES_OAEP_SHA_256
&CertificateId=12345678-1234-1234-1234-12345678****
&CiphertextBlob=ZOyIygCyaOW6Gj****MlNKiuyjfzw=
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
        <CertificateId>12345678-1234-1234-1234-12345678****</CertificateId>
        <Plaintext>VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4</Plaintext>
        <RequestId>5979d897-d69f-4fc9-87dd-f3bb73c40b80</RequestId>
</KMS>
```

`JSON`格式

```
{
  "CertificateId": "12345678-1234-1234-1234-12345678****",
  "Plaintext": "VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4",
  "RequestId": "5979d897-d69f-4fc9-87dd-f3bb73c40b80"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Certificate.NotFound|The specified certificate is not found.|指定的证书不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

