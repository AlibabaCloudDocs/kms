# CreateCertificate

调用CreateCertificate接口创建证书。

创建证书时，请指定非对称密钥的类型，将私钥托管在证书管家，并获取证书请求CSR（Certificate Signing Request）。然后将PEM格式的证书请求文件提交给CA机构，获取正式的证书和证书链，并调用[UploadCertificate](~~212136~~)接口导入证书管家。

本文将提供一个示例，创建一个证书，并获取证书请求CSR。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateCertificate|要执行的操作，取值：CreateCertificate。 |
|KeySpec|String|是|RSA\_2048|密钥类型，取值：

 -   RSA\_2048
-   EC\_P256
-   EC\_SM2 |
|Subject|String|是|CN=userName,OU=kms,O=aliyun,C=CN|证书主体（拥有者）。

 按照[RFC 2253](https://tools.ietf.org/html/rfc2253?spm=a2c4g.11186623.2.13.265f1a1cGFCn3Q)定义，采用DN（Distinguished Names）标识。DN由一系列RDN（Relative Distinguished Names）组成。

 RDN是一组键值对，多个RDN之间用英文逗号（,）隔开，格式为：`attribute1=value1,attribute2=value2`。

 证书主体字段含义如下：

 -   CN（必选）：名称。证书使用主体名称。
-   C（必选）：国家/地区。使用[ISO 3166-1](https://www.iso.org/obp/ui/#search/code/)的二位国家代码。例如：CN代表中国。
-   O（必选）：公司名称。企业、单位、组织或机构的法定名称。
-   OU（必选）：部门名称。
-   ST（可选）：省/市。省、直辖市、自治区或特别行政区名称。
-   L（可选）：城市名称。 |
|SubjectAlternativeNames|Json|否|\["test1.example.com","test2.example.com"\]|证书主体别名。

 支持域名列表，最多支持10个域名。 |
|ExportablePrivateKey|Boolean|否|true|证书私钥是否需要导出使用。取值：

 -   true（默认值）：证书私钥需要导出使用。
-   false：证书私钥不需要导出使用。建议选择否，以便使用更高安全级别的密钥保护。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:certificate/98e85c94-52d0-40c9-b3b2-afda52f4\*\*\*\*|证书ARN。 |
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

`XML`格式

```
<KMS>
	  <CertificateId>98e85c94-52d0-40c9-b3b2-afda52f4****</CertificateId>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:certificate/98e85c94-52d0-40c9-b3b2-afda52f4****</Arn>
	  <Csr>-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----</Csr>
	  <RequestId>15a735a1-8fe6-45cc-a64c-3c4ff839334e</RequestId>
</KMS>
```

`JSON`格式

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

