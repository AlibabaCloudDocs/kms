# CreateCertificate

调用CreateCertificate接口创建证书。

创建时您需要指定非对称密钥的类型，将私钥托管在证书管家，并生成证书签发请求CSR（Certificate Signing Request）。您需要将CSR提交给您选定的证书签发系统，并将此系统根据CSR签发的证书和关联的证书链导入回证书管家。

本文将提供一个示例，创建一个ID为`98e85c94-52d0-40c9-b3b2-afda52f4****`的证书，并返回证书签发请求CSR。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateCertificate|要执行的操作，取值：CreateCertificate。 |
|KeySpec|String|是|RSA\_2048|密钥的类型，取值：

 -   RSA\_2048
-   EC\_P256
-   EC\_SM2 |
|Subject|String|是|CN=userName,OU=kms,O=aliyun,C=CN|证书主体（拥有者）。

 按照[RFC 2253](https://tools.ietf.org/html/rfc2253?spm=a2c4g.11186623.2.13.265f1a1cGFCn3Q)定义，采用DN（Distinguished Names）标识。DN由一系列RDN（Relative Distinguished Names）组成。

 RDN是一组键值对，多个RDN之间用英文逗号（,）隔开，格式为：`attribute1=value1,attribute2=value2`。 |
|SubjectAlternativeNames|Json|否|\["test1.example.com","test2.example.com"\]|证书主体别名。

 支持域名列表，最多支持10个域名。 |
|ProtectionLevel|String|否|SOFTWARE|证书私钥的保护级别，取值：

 -   SOFTWARE（默认值）
-   HSM

 **说明：** HSM保护级别仅在支持托管密码机的地域支持。更多信息，请参见[支持的地域](~~125803~~)。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:certificate/98e85c94-52d0-40c9-b3b2-afda52f4\*\*\*\*|阿里云资源名称。 |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|Csr|String|-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY\*\*\*\*-----END CERTIFICATE REQUEST-----|PEM格式的证书请求。 |
|RequestId|String|15a735a1-8fe6-45cc-a64c-3c4ff839334e|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateCertificate
&KeySpec=RSA_2048
&Subject=CN=userName,OU=kms,O=aliyun,C=CN
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
	  <CertificateId>98e85c94-52d0-40c9-b3b2-afda52f4****</CertificateId>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:certificate/98e85c94-52d0-40c9-b3b2-afda52f4****</Arn>
	  <Csr>-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----</Csr>
	  <RequestId>15a735a1-8fe6-45cc-a64c-3c4ff839334e</RequestId>
</KMS>
```

`JSON` 格式

```
{
	"CertificateId": "98e85c94-52d0-40c9-b3b2-afda52f4****",
	"Arn": "acs:kms:cn-hangzhou:154035569884****:certificate/98e85c94-52d0-40c9-b3b2-afda52f4****",
	"Csr": "-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----",
	"RequestId": "15a735a1-8fe6-45cc-a64c-3c4ff839334e"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|AccessKey ID找不到。请检查调用时是否使用了正确的AccessKey。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

