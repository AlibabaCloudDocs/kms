# UpdateCertificateStatus

调用UpdateCertificateStatus接口更新证书状态。

本文将提供一个示例，将ID为`9a28de48-8d8b-484d-a766-dec4****`证书的状态更新为已禁用。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateCertificateStatus&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateCertificateStatus|要执行的操作，取值：UpdateCertificateStatus。 |
|CertificateId|String|是|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|证书ID。证书管家中证书的全局唯一标识符。 |
|Status|String|是|DISABLED|证书的状态，取值：

 -   DISABLED：已禁用。
-   ACTIVE：已启用。
-   REOVKED：已吊销。

**说明：** 当证书状态为REOVKED（已吊销）时，不能进行签名操作，只能进行验签操作。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|e3f57fe0-9ded-40b0-9caf-a3815f2148c1|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateCertificateStatus
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&Status=DISABLED
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
	  <RequestId>e3f57fe0-9ded-40b0-9caf-a3815f2148c1</RequestId>
 </KMS>
```

`JSON` 格式

```
{
	"RequestId": "e3f57fe0-9ded-40b0-9caf-a3815f2148c1"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|404|Certificate.NotFound|The specified certificate is not found.|指定的证书不存在。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

