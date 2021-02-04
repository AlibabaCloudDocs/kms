# RotateSecret

调用RotateSecret接口手动轮转凭据。

使用限制：

• 同一阿里云账号每小时最多轮转50次。

• RotateSecret接口不支持轮转普通凭据。

本文将提供一个示例，将名称为`RdsSecret/Mysql5.4/MyCred`的凭据进行手动轮转，轮转后新的凭据版本为`000000123`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=RotateSecret&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|RotateSecret|要执行的操作，取值：RotateSecret。 |
|SecretName|String|是|RdsSecret/Mysql5.4/MyCred|凭据名称。 |
|VersionId|String|是|000000123|轮转后的凭据新版本的版本号。

 **说明：** 版本号用于保证请求的幂等性。凭据管家使用版本号来防止您的应用在请求失败后进行重试时，意外创建重复的版本。如果相同的版本号已经存在，轮转的请求会被忽略，服务端会返回成功。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/RdsSecret/Mysql5.4/MyCred|凭据ARN。 |
|SecretName|String|RdsSecret/Mysql5.4/MyCred|凭据名称。 |
|VersionId|String|000000123|轮转后的凭据新版本的版本号。 |
|RequestId|String|10257c86-269d-43aa-aaf3-90ed4144bb7c|请求ID。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=RotateSecret
&SecretName=RdsSecret/Mysql5.4/MyCred
&VersionId=000000123
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:secret/RdsSecret/Mysql5.4/MyCred</Arn>
	  <SecretName>RdsSecret/Mysql5.4/MyCred</SecretName>
	  <VersionId>000000123</VersionId>
	  <RequestId>10257c86-269d-43aa-aaf3-90ed4144bb7c</RequestId>
</KMS>
```

`JSON`格式

```
{
	"Arn": "acs:kms:cn-hangzhou:154035569884****:secret/RdsSecret/Mysql5.4/MyCred",
	"SecretName": "RdsSecret/Mysql5.4/MyCred",
	"VersionId": "000000123",
	"RequestId": "10257c86-269d-43aa-aaf3-90ed4144bb7c"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

