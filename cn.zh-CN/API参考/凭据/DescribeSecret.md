# DescribeSecret

调用DescribeSecret接口查询凭据的元数据信息。

此接口返回指定凭据的元数据信息，不返回被加密存储的凭据值。

本文将提供一个示例，返回一个名称为`secret001`凭据的元数据信息，包括凭据ARN、凭据名称、类型、描述、创建和更新时间、自动轮转信息以及拓展配置。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DescribeSecret&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeSecret|要执行的操作，取值：DescribeSecret。 |
|SecretName|String|是|secret001|凭据名称。 |
|FetchTags|String|否|true|是否在返回参数中包含凭据的资源标签。取值：

 -   true：包含资源标签。
-   false（默认值）：不包含资源标签。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/secret001|凭据ARN。 |
|AutomaticRotation|String|Enabled|是否开启自动轮转。取值：

 -   Enabled：开启自动轮转。
-   Disabled：不开启自动轮转。
-   Invalid：轮转状态异常，凭据管家无法为您自动轮转。

 **说明：** 仅托管RDS凭据返回该参数。 |
|CreateTime|String|2020-02-21T15:39:26Z|创建凭据的时间。 |
|Description|String|userinfo|凭据的描述信息。 |
|EncryptionKeyId|String|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|用于加密保护凭据值的KMS主密钥的标识符。 |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|凭据的拓展配置。

 **说明：** 仅托管RDS凭据返回该参数。 |
|LastRotationDate|String|2020-07-05T08:22:03Z|最近一次轮转的时间。

 **说明：** 当凭据发生过轮转时返回该参数。 |
|NextRotationDate|String|2020-07-06T18:22:03Z|下一次轮转的时间。

 **说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|PlannedDeleteTime|String|2020-03-21T15:45:12Z|计划删除时间。 |
|RequestId|String|93348dfb-3627-4417-8d90-487a76a909c9|请求ID。 |
|RotationInterval|String|3153600s|凭据自动轮转的周期。

 格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。 `unit`取值：s（秒）。例如：7天的轮转周期为604800s。

 **说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|SecretName|String|secret001|凭据名称。 |
|SecretType|String|Rds|凭据类型。取值：

 -   Generic：普通凭据。
-   Rds：托管RDS凭据。 |
|Tags|Array of Tag| |凭据的资源标签。

 如果FetchTags取值为false或者未指定，则不返回该参数。 |
|Tag| | | |
|TagKey|String|key1|标签键。 |
|TagValue|String|val1|标签值。 |
|UpdateTime|String|2020-02-21T15:39:26Z|更新时间。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeSecret
&SecretName=secret001
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:secret/secret001</Arn>
	  <SecretName>secret001</SecretName>
	  <Description>userinfo</Description>
	  <CreateTime>2021-01-08T10:50:05Z</CreateTime>
	  <UpdateTime>2021-01-08T10:50:05Z</UpdateTime>
	  <RequestId>93f84812-66d2-467a-9aec-61f6f53919dc</RequestId>
	  <SecretType>Rds</SecretType>
	  <AutomaticRotation>Disabled</AutomaticRotation>
	  <ExtendedConfig>{"SecretSubType":"SingleUser", "DBInstanceId":"rm-uf667446pc955****",  "CustomData":{} }</ExtendedConfig>
</KMS>
```

`JSON`格式

```
{
	"Arn": "acs:kms:cn-hangzhou:154035569884****:secret/secret001",
	"SecretName": "secret001",
	"Description": "userinfo",
	"CreateTime": "2021-01-08T10:50:05Z",
	"UpdateTime": "2021-01-08T10:50:05Z",
	"RequestId": "93f84812-66d2-467a-9aec-61f6f53919dc",
	"SecretType": "Rds",
	"AutomaticRotation": "Disabled",
	"ExtendedConfig": "{\"SecretSubType\":\"SingleUser\", \"DBInstanceId\":\"rm-uf667446pc955****\",  \"CustomData\":{} }"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

