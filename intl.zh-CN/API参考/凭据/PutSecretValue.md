# PutSecretValue

调用PutSecretValue接口为凭据存入一个新版本的凭据值。

此接口用于存入新版本的凭据值，而不能用于修改已有版本的凭据值。

默认情况下，新存入的凭据值被标记为ACSCurrent，而ACSCurrent标记的前一个版本被标记为ACSPrevious。您可以通过指定VersionStage参数来覆盖该默认行为。

存入新版本时需指定版本号，凭据管家按照如下规则进行操作：

-   如果指定版本号在凭据内并不存在，则创建新版本并存入凭据值。
-   如果指定版本号在凭据内已经存在，且关联的凭据值和参数中指定的凭据值相等，则请求会被忽略，并且返回成功（请求是幂等的）。
-   如果指定版本号在凭据内已经存在，但是关联的凭据值和参数中指定的凭据值并不相等，则请求会被拒绝，且返回失败。

使用限制：该接口仅支持普通凭据。

本文将提供一个示例，为名为`secret001`的凭据存入一个新版本的凭据值，新凭据版本号`VersionId`为`00000000000000000000000000000000203`、凭据值`SecretData`为`importantdata`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=PutSecretValue&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|PutSecretValue|要执行的操作，取值：PutSecretValue。 |
|SecretData|String|是|importantdata|凭据值。加密后存入指定的新版本中。 |
|SecretName|String|是|secret001|凭据名称。 |
|VersionId|String|是|00000000000000000000000000000000203|新凭据版本的版本号。凭据对象内版本号唯一。 |
|SecretDataType|String|否|text|凭据值类型。取值：

 -   text（默认值）
-   binary |
|VersionStages|String|否|\{"VersionStage": \[ "ACSCurrent" \] \}|凭据版本在存入时需要被同时标记的版本状态。如果您不指定此参数，凭据管家默认为新版本标记ACSCurrent。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8|请求ID。 |
|SecretName|String|secret001|凭据名称。 |
|VersionId|String|00000000000000000000000000000000203|被存入凭据版本的版本号。 |
|VersionStages|List|\{"VersionStage": \["ACSCurrent"\]\}|版本被标记的状态。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=PutSecretValue
&SecretData=importantdata
&SecretName=secret001
&VersionId=00000000000000000000000000000000203
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <VersionId>00000000000000000000000000000000203</VersionId>
	  <VersionStages>
		    <VersionStage>ACSCurrent</VersionStage>
	  </VersionStages>
	  <RequestId>f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8</RequestId>
</KMS>
```

`JSON`格式

```
{
	"SecretName": "secret001",
	"VersionId": "00000000000000000000000000000000203",
	"VersionStages": {
		"VersionStage": [
			"ACSCurrent"
		]
	},
	"RequestId": "f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

