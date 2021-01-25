# DeleteCertificate

调用DeleteCertificate接口删除证书及其对应的私钥和证书链。

证书及其对应的私钥和证书链删除后将无法恢复，请谨慎操作。

本文将提供一个示例，删除ID为`9a28de48-8d8b-484d-a766-dec4****`的证书及其对应的私钥和证书链。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DeleteCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteCertificate|要执行的操作，取值：DeleteCertificate。 |
|CertificateId|String|是|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DeleteCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
	  <RequestId>d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0</RequestId>
</KMS>
```

`JSON` 格式

```
{
	"RequestId": "d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Certificate.NotFound|The specified certificate is not found.|指定的证书不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

