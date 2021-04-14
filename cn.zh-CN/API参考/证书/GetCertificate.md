# GetCertificate

调用GetCertificate接口查询证书管家托管的证书。

本文将提供一个示例，查询ID为`9a28de48-8d8b-484d-a766-dec4****`的证书信息，包括证书、证书链、证书ID和证书请求。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=GetCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetCertificate|要执行的操作，取值：GetCertificate。 |
|CertificateId|String|是|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Certificate|String|-----BEGIN CERTIFICATE----- \(X.509 Certificate PEM Content\) -----END CERTIFICATE-----|PEM格式的证书。 |
|CertificateChain|String|-----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Root CA Certificate PEM Content\) -----END CERTIFICATE-----|PEM格式的证书链。 |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。 |
|Csr|String|-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY\*\*\*\*-----END CERTIFICATE REQUEST-----|PEM格式的证书请求。 |
|RequestId|String|b3e104b4-0319-4a20-ab7f-9fef6\*\*\*\*|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <Csr>-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----</Csr>
	  <RequestId>b3e104b4-0319-4a20-ab7f-9fef6****</RequestId>
	  <CertificateId>9a28de48-8d8b-484d-a766-dec4****</CertificateId>
	  <CertificateChain>-----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Root CA Certificate PEM Content)  -----END CERTIFICATE-----</CertificateChain>
	  <Certificate>-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----</Certificate>
</KMS>
```

`JSON`格式

```
{
	"Csr": "-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----",
	"RequestId": "b3e104b4-0319-4a20-ab7f-9fef6****",
	"CertificateId": "9a28de48-8d8b-484d-a766-dec4****",
	"CertificateChain": "-----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Root CA Certificate PEM Content)  -----END CERTIFICATE-----",
	"Certificate": "-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|AccessKey ID找不到。请检查调用时是否使用了正确的AccessKey。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

