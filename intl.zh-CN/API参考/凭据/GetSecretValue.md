# GetSecretValue

调用GetSecretValue接口获取凭据值。

如果不指定版本号或版本状态，则凭据管家默认返回被标记为ACSCurrent的版本凭据值。

如果凭据使用了用户指定的主密钥来保护凭据值，则需要调用者同时具备相应主密钥的`kms:Decrypt`权限。

本文将提供一个示例，获取一个名为`secret001`凭据的凭据值，返回结果显示凭据值`SecretData`为`testdata1`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=GetSecretValue&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|GetSecretValue|要执行的操作，取值：GetSecretValue。 |
|SecretName|String|是|secret001|凭据名称。 |
|VersionStage|String|否|ACSCurrent|版本状态。如果指定该参数，则凭据管家返回被标记为指定状态的版本的凭据值。

 默认值：ACSCurrent。

 **说明：** 托管RDS凭据只能获取ACSPrevious和ACSCurrent对应版本的凭据值。 |
|VersionId|String|否|00000000000000000000000000000001|版本号。如果指定该参数，则凭据管家返回指定版本号的凭据值。

 **说明：** 托管RDS凭据不支持指定VersionId，设置该参数将被忽略。 |
|FetchExtendedConfig|Boolean|否|true|是否获取凭据的拓展配置。取值：

 -   true
-   false（默认值）

 **说明：** 普通凭据设置该参数将被忽略。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AutomaticRotation|String|Enabled|是否开启自动轮转。取值：

 -   Enabled：开启自动轮转。
-   Disabled：不开启自动轮转。
-   Invalid：轮转状态异常，凭据管家无法为您自动轮转。

 **说明：** 仅托管RDS凭据返回该参数。 |
|CreateTime|String|2020-02-21T15:39:26Z|创建凭据的时间。 |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|凭据的拓展配置。当SecretType取值为Rds，且FetchExtendedConfig取值为true时返回该参数。 |
|LastRotationDate|String|2020-07-05T08:22:03Z|最近一次轮转的时间。

 **说明：** 当凭据发生过轮转时返回该参数。 |
|NextRotationDate|String|2020-07-06T18:22:03Z|下一次轮转的时间。

 **说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|RequestId|String|6a3e9c36-1150-4881-84d3-eb8672fcafad|请求ID。 |
|RotationInterval|String|604800s|凭据自动轮转的周期。

 格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。 `unit`取值：s（秒）。例如：7天的轮转周期为604800s。

 **说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|SecretData|String|testdata1|凭据值。凭据管家将存储的密文凭据值进行解密后返回该参数。

 托管RDS凭据返回的凭据值满足以下格式：

 `{"AccountName":"","AccountPassword":""}`|
|SecretDataType|String|binary|凭据值类型。取值：

 -   text
-   binary |
|SecretName|String|secret001|凭据名称。 |
|SecretType|String|Generic|凭据类型。取值：

 -   Generic：普通凭据。
-   Rds：托管RDS凭据。 |
|VersionId|String|00000000000000000000000000000001|凭据版本的标识符。 |
|VersionStages|List|\{ "VersionStage": \[ "ACSCurrent" \] \}|凭据版本的状态标记。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=GetSecretValue
&SecretName=secret001
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <VersionId>00000000000000000000000000000001</VersionId>
	  <SecretData>testdata1</SecretData>
	  <SecretType>Generic</SecretType>
	  <SecretDataType>binary</SecretDataType>
	  <VersionStages>
		    <VersionStage>ACSCurrent</VersionStage>
	  </VersionStages>
	  <CreateTime>2020-07-23T11:56:29Z</CreateTime>
	  <RequestId>6a3e9c36-1150-4881-84d3-eb8672fcafad</RequestId>
</KMS>
```

`JSON`格式

```
{
	"SecretName": "secret001",
	"VersionId": "00000000000000000000000000000001",
	"SecretData": "testdata1",
	"SecretType": "Generic",
	"SecretDataType": "binary",
	"VersionStages": {
		"VersionStage": [
			"ACSCurrent"
		]
	},
	"CreateTime": "2020-07-23T11:56:29Z",
	"RequestId": "6a3e9c36-1150-4881-84d3-eb8672fcafad"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

