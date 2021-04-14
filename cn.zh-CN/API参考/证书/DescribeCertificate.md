# DescribeCertificate

调用DescribeCertificate接口查询证书信息。

本文将提供一个示例，查询一个ID为`9a28de48-8d8b-484d-a766-dec4****`的证书信息，包括证书ID、创建时间、签发者信息、有效期、序列号、签名算法等。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DescribeCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeCertificate|要执行的操作，取值：DescribeCertificate。 |
|CertificateId|String|是|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:159498693826\*\*\*\*:certificate/9a28de48-8d8b-484d-a766-dec4\*\*\*\*"|证书ARN。 |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|CreatedAt|String|2020-10-13T03:05:03Z|证书的创建时间。 |
|ExportablePrivateKey|Boolean|true|证书密钥是否支持导出。取值：

 -   true（默认值）：支持导出。
-   false：不支持导出。 |
|Issuer|String|CN=testCA,OU=kms,O=aliyun,C=CN|证书的签发者信息，使用限定名DN（Distinguished Names）形式标识。 |
|KeySpec|String|RSA\_2048|密钥类型。 |
|NotAfter|String|2022-10-13T03:09:00Z|证书有效期的截止时间。 |
|NotBefore|String|2020-10-13T03:09:00Z|证书有效期的开始时间。 |
|RequestId|String|edb671a3-c5a1-4ebe-a1de-d748b640bdf2|请求ID。 |
|Serial|String|12345678|证书序列号。 |
|SignatureAlgorithm|String|ECDSA-SHA256|证书签名算法，取值：

 -   RSA2048-SHA256
-   ECDSA-SHA256
-   SM2-SM3 |
|Status|String|ACTIVE|证书的状态信息，取值：

 -   PENDING：等待导入。
-   ACTIVE：已启用。
-   DISABLE：已禁用。
-   REVOKED：已吊销。 |
|Subject|String|CN=userName,OU=aliyun,O=aliyun,C=CN|证书主体（拥有者） ，采用DN标识。 |
|SubjectAlternativeNames|List|\["test1.example.com","test2.example.com"\]|证书主体别名。

 支持域名列表，最多支持10个域名。 |
|SubjectKeyIdentifier|String|79 36 26 DE 9F F5 15 E3 56 DC \*\*\*\*|主体公钥识别符。 |
|SubjectPublicKey|String|-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----|证书中的公钥。 |
|Tags|Map|\[\{\\"TagKey\\":\\"S1key1\\",\\"TagValue\\":\\"S1val1\\"\},\{\\"TagKey\\":\\"S1key2\\",\\"TagValue\\":\\"S2val2\\"\}\]|证书对应的标签。 |
|UpdatedAt|String|2020-12-23T06:10:13Z|证书的更新时间。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <Status>ACTIVE</Status>
	  <RequestId>edb671a3-c5a1-4ebe-a1de-d748b640bdf2</RequestId>
	  <Issuer>CN=testCA,OU=kms,O=aliyun,C=CN</Issuer>
	  <CertificateId>9a28de48-8d8b-484d-a766-dec4****</CertificateId>
	  <CreatedAt>2020-10-13T03:05:03Z</CreatedAt>
	  <KeySpec>RSA_2048</KeySpec>
	  <SubjectAlternativeNames>[\"test1.example.com\",\"test2.example.com\"]</SubjectAlternativeNames>
	  <SignatureAlgorithm>ECDSA-SHA256</SignatureAlgorithm>
	  <SubjectKeyIdentifier>79 36 26 DE 9F F5 15 E3 56 DC ********</SubjectKeyIdentifier>
	  <NotAfter>2022-10-13T03:09:00Z</NotAfter>
      <ExportablePrivateKey>true</ExportablePrivateKey>
	  <UpdatedAt>2020-10-13T03:15:00Z</UpdatedAt>
	  <Subject>CN=userName,OU=aliyun,O=aliyun,C=CN</Subject>
	  <Serial>12345678</Serial>
	  <SubjectPublicKey>-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----</SubjectPublicKey>
	  <NotBefore>2020-10-13T03:09:00Z</NotBefore>
	  <Arn>acs:kms:cn-hangzhou:159498693826****:certificate/9a28de48-8d8b-484d-a766-dec4****</Arn>
	  <Tags>[{\"TagKey\":\"S1key1\",\"TagValue\":\"S1val1\"},{\"TagKey\":\"S1key2\",\"TagValue\":\"S2val2\"}]</Tags>
</KMS>
```

`JSON`格式

```
{
    "Status": "ACTIVE",
    "RequestId": "edb671a3-c5a1-4ebe-a1de-d748b640bdf2",
    "Issuer": "CN=testCA,OU=kms,O=aliyun,C=CN",
    "CertificateId": "9a28de48-8d8b-484d-a766-dec4****",
    "CreatedAt": "2020-10-13T03:05:03Z",
    "KeySpec": "RSA_2048",
    "SubjectAlternativeNames": "[\"test1.example.com\",\"test2.example.com\"]",
    "SignatureAlgorithm": "ECDSA-SHA256",
    "SubjectKeyIdentifier": "79 36 26 DE 9F F5 15 E3 56 DC ********",
    "NotAfter": "2022-10-13T03:09:00Z",
    "ExportablePrivateKey": "true",
    "UpdatedAt": "2020-10-13T03:15:00Z",
    "Subject": "CN=userName,OU=aliyun,O=aliyun,C=CN",
    "Serial": "12345678",
    "SubjectPublicKey": "-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----",
    "NotBefore": "2020-10-13T03:09:00Z",
    "Arn": "acs:kms:cn-hangzhou:159498693826****:certificate/9a28de48-8d8b-484d-a766-dec4****",
    "Tags": "[{\"TagKey\":\"S1key1\",\"TagValue\":\"S1val1\"},{\"TagKey\":\"S1key2\",\"TagValue\":\"S2val2\"}]"
 }
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Certificate.NotFound|The specified certificate is not found.|指定的证书不存在。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

