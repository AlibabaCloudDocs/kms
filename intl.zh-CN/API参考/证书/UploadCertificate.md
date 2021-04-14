# UploadCertificate

调用UploadCertificate接口将CA机构颁发的证书和证书链导入证书管家。

本文将提供一个示例，将CA机构颁发的证书导入到KMS证书管家中ID为`12345678-1234-1234-1234-12345678****`的证书中。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UploadCertificate&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UploadCertificate|要执行的操作，取值：UploadCertificate。 |
|Certificate|String|是|-----BEGIN CERTIFICATE----- \(X.509 Certificate PEM Content\) -----END CERTIFICATE-----|CA机构颁发的PEM格式的证书。 |
|CertificateId|String|是|12345678-1234-1234-1234-12345678\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|CertificateChain|String|否|-----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Root CA Certificate PEM Content\) -----END CERTIFICATE-----|CA机构颁发的PEM格式的证书链。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|15a735a1-8fe6-45cc-a64c-3c4ff839334e|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UploadCertificate
&Certificate=-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----
&CertificateId=12345678-1234-1234-1234-12345678****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
        <RequestId>15a735a1-8fe6-45cc-a64c-3c4ff839334e</RequestId>
</KMS>
```

`JSON`格式

```
{
    "RequestId": "15a735a1-8fe6-45cc-a64c-3c4ff839334e"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|AccessKey ID找不到。请检查调用时是否使用了正确的AccessKey。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

