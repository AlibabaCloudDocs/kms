# CertificatePrivateKeySign

调用CertificatePrivateKeySign接口使用指定证书生成数字签名。

使用限制：请求参数中签名算法需要跟密钥类型对应。

签名算法和密钥类型对照表如下：

|Algorithm

|Key Spec |
|-----------|----------|
|RSA\_PKCS1\_SHA\_256

|RSA\_2048 |
|RSA\_PSS\_SHA\_256

|RSA\_2048 |
|ECDSA\_SHA\_256

|EC\_P256 |
|SM2DSA

|EC\_SM2

| |

本文将提供一个示例，使用ID为`12345678-1234-1234-1234-12345678****`的证书，通过`ECDSA_SHA_256`签名算法为原始数据`VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=`生成数字签名。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CertificatePrivateKeySign&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CertificatePrivateKeySign|要执行的操作，取值：CertificatePrivateKeySign。 |
|Algorithm|String|是|ECDSA\_SHA\_256|签名算法。取值：

 -   RSA\_PKCS1\_SHA\_256
-   RSA\_PSS\_SHA\_256
-   ECDSA\_SHA\_256
-   SM2DSA

**说明：** SM2DSA签名算法仅在中国内地使用托管密码机的地域支持。更多信息，请参见[托管密码机概述](~~125803~~)。 |
|CertificateId|String|是|12345678-1234-1234-1234-12345678\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|Message|String|是|VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=|待签名数据。

 使用Base64编码。例如：待签名数据的十六进制内容为`[0x31, 0x32, 0x33, 0x34]`，则对应的Base64编码为`MTIzNA==`。

 当MessageType取值为RAW时，数据内容需小于4KB。

 如果待签名数据内容大于4KB，您可以将MessageType指定为DIGEST，将Message指定为本地计算的消息摘要（又称哈希值）。证书管家将使用您自己的证书应用系统计算消息摘要，使用的消息摘要算法须与指定签名算法需要的消息摘要算法保持一致。具体如下：

 -   RSA\_PKCS1\_SHA\_256、RSA\_PSS\_SHA\_256和ECDSA\_SHA\_256对应的消息摘要算法为SHA-256。
-   SM2DSA对应的消息摘要算法为SM3。

 **说明：** 当证书密钥规格为EC\_SM2，并且MessageType为DIGEST时，Message值为GB/T 32918.2-2016 6.1中描述的`e`。 |
|MessageType|String|是|RAW|消息类型。取值：

 -   RAW（默认值）：原始数据。
-   DIGEST：原始数据的消息摘要（哈希值）。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|CertificateId|String|12345678-1234-1234-1234-12345678\*\*\*\*|证书ID。 |
|RequestId|String|5979d897-d69f-4fc9-87dd-f3bb73c40b80|请求ID。 |
|SignatureValue|String|ZOyIygCyaOW6Gj\*\*\*\*MlNKiuyjfzw=|签名值。

 使用Base64编码。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CertificatePrivateKeySign
&Algorithm=ECDSA_SHA_256
&CertificateId=12345678-1234-1234-1234-12345678****
&Message=VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=
&MessageType=RAW
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <CertificateId>12345678-1234-1234-1234-123456789012</CertificateId>
	  <SignatureValue>ZOyIygCyaOW6Gj****MlNKiuyjfzw=</SignatureValue>
	  <RequestId>5979d897-d69f-4fc9-87dd-f3bb73c40b80</RequestId>
</KMS>
```

`JSON`格式

```
{
  "CertificateId": "12345678-1234-1234-1234-123456789012",
  "SignatureValue": "ZOyIygCyaOW6Gj****MlNKiuyjfzw=",
  "RequestId": "5979d897-d69f-4fc9-87dd-f3bb73c40b80"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Certificate.NotFound|The specified certificate is not found.|指定的证书不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

