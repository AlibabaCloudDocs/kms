# CreateSecret

调用CreateSecret接口创建凭据，并存入凭据的初始版本。

您需要指定凭据名称、初始版本的凭据值和版本号。初始版本的状态被标记为ACSCurrent。

您可以指定一个对称密钥类型的用户主密钥（CMK）作为保护凭据的加密密钥。当不指定CMK时，凭据管家将为您自动创建一个主密钥，用于默认加密您的阿里云账号在本地域创建的凭据。凭据管家加密每个版本的凭据值，凭据名称、版本号、版本的状态标记等元数据不会被加密。

如果您指定主密钥，则需要同时具备相应主密钥的`kms:GenerateDataKey`权限，用于对凭据值进行加密。

本文将提供一个示例，创建一个名称为`mydbconninfo`、初始版本号`VersionId`为`v1`、凭据值`SecretData`为`{"user":"root","passwd":"****"}`的普通凭据。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateSecret&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSecret|要执行的操作，取值：CreateSecret。 |
|SecretData|String|是|\{"user":"root","passwd":"\*\*\*\*"\}|新创建凭据的凭据值。凭据管家将其加密后，存入初始版本中。

-   创建普通凭据时，您可以根据需要指定凭据值。
-   创建托管RDS凭据时，凭据值格式为：`{"Accounts":[{"AccountName":"","AccountPassword":""}]}`。其中，`AccountName`为RDS实例的账号名称，`AccountPassword`为RDS实例的账号口令。 |
|SecretName|String|是|mydbconninfo|凭据名称。 |
|VersionId|String|是|v1|初始版本的版本号。凭据对象内版本号唯一。 |
|EncryptionKeyId|String|否|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|用于加密保护凭据值的KMS主密钥的标识符。

如果不指定，则凭据管家使用系统创建的密钥来加密保护凭据数据。

**说明：** KMS主密钥必须是对称密钥。 |
|SecretDataType|String|否|text|凭据值类型。取值：

-   text
-   binary

**说明：** 创建托管RDS凭据时，SecretDataType取值只能为text。 |
|Description|String|否|mydbinfo|凭据的描述信息。 |
|Tags|String|否|\[\{\\"TagKey\\":\\"key1\\",\\"TagValue\\":\\"val1\\"\},\{\\"TagKey\\":\\"key2\\",\\"TagValue\\":\\"val2\\"\}\]|凭据的标签。 |
|SecretType|String|否|Rds|凭据类型。取值：

-   Generic：普通凭据。
-   Rds：托管RDS凭据。 |
|ExtendedConfig|Json|否|\{"SecretSubType":"SingleUser", "DBInstanceId":"rm-bp1b3dd3a506e\*\*\*\*" ,"CustomData":\{\}\}|凭据的拓展配置，用于指定特定凭据类型的属性。长度不超过1024个字符，格式为JSON Map。

-   当SecretType取值为Generic时，忽略该参数。
-   当SecretType取值为Rds时，需要指定ExtendedConfig的如下参数：
    -   SecretSubType（必填）：凭据子类型。取值：
        -   SingleUser：指定凭据管家以单账号模式托管RDS凭据。凭据轮转时，指定账号的口令会被重置为新的随机口令。
        -   DoubleUsers：指定凭据管家以双账号模式托管RDS凭据，ACSCurrent和ACSPrevious分别引用其中一个账号。凭据轮转时，ACSPrevious引用账号的口令会被重置为新的随机口令，随后凭据管家交换ACSCurrent和ACSPrevious对RDS账号的引用。
    -   DBInstanceId（必填）：指定RDS账号所在的RDS实例。
    -   CustomData（可选）：自定义数据。取值为JSON格式的键值对，最多不超过10个键值对，多个键值对直接用英文逗号（,）间隔。取值示例：`{"Key1": "v1", "fds":"fdsf"}`。默认值为空`{}`。 |
|EnableAutomaticRotation|Boolean|否|true|是否开启自动轮转，取值：

-   true：开启自动轮转。
-   false（默认值）：不开启自动轮转。

**说明：** 当SecretType取值为Rds时该参数有效。 |
|RotationInterval|String|否|30d|自动轮转的周期。取值范围：6小时~8,760小时（365天）。

格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。

unit取值：d（天）、h（小时）、m（分钟）、s（秒）。例如：7d或者604,800s均表示7天的周期。

**说明：** 当EnableAutomaticRotation取值为true时，必须设置该参数。反之，将忽略该参数。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/mydbconninfo|阿里云资源名称。 |
|AutomaticRotation|String|Enabled|是否开启自动轮转。取值：

-   Enabled：开启自动轮转。
-   Disabled：不开启自动轮转。
-   Invalid：轮转状态异常，凭据管家无法为您自动轮转。

**说明：** 当SecretType取值为Rds时，返回该参数。 |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|凭据的拓展配置。当SecretType取值为Rds时返回该参数。 |
|NextRotationDate|String|2020-07-06T18:22:03Z|下一次轮转的时间。

**说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|RequestId|String|3bf02f7a-015b-4f93-be0f-cc043fda2dd3|请求ID。 |
|RotationInterval|String|604800s|凭据自动轮转的周期。

格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。 `unit`取值：s（秒）。例如：7天的轮转周期为604800s。

**说明：** 当AutomaticRotation取值为Enabled或Invalid时，返回该参数。 |
|SecretName|String|mydbconninfo|凭据名称。 |
|SecretType|String|Rds|凭据类型。 |
|VersionId|String|v1|凭据版本号。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateSecret
&SecretData={"user":"root","passwd":"****"}
&SecretName=mydbconninfo
&VersionId=v1
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
      <Arn>acs:kms:cn-hangzhou:154035569884****:secret/mydbconninfo</Arn>
      <SecretName>mydbconninfo</SecretName>
      <VersionId>v1</VersionId>
      <RequestId>3bf02f7a-015b-4f93-be0f-cc043fda2dd3</RequestId>
      <SecretType>Generic</SecretType>
 </KMS>
```

`JSON`格式

```
{
    "Arn": "acs:kms:cn-hangzhou:154035569884****:secret/mydbconninfo",
    "SecretName": "mydbconninfo",
    "VersionId": "v1",
    "RequestId": "3bf02f7a-015b-4f93-be0f-cc043fda2dd3",
    "SecretType": "Generic"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|InvalidParameter|The specified parameter is invalid.|参数错误。|
|400|Rejected.LimitExceeded|The secret quota is exceeded.|凭据超出配额。|
|403|Forbidden.NoPermission|You are not authorized to perform the operation.|操作无权限。|
|404|Forbidden.ResourceNotFound|The resource is not found.|资源不存在。|
|409|Rejected.ResourceExist|The resource already exists.|资源已存在。|
|409|Rejected.ResourceInDeleteWindow|The secret is planned to be deleted.|此凭据在计划删除中。|
|500|InternalFailure|An internal error occurred.|内部错误。|
|429|Rejected.Throttling|The QPS upper limit is exceeded.|限流达到上限。|

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

