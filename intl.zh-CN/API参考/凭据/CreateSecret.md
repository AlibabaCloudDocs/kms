# CreateSecret

调用CreateSecret接口创建凭据，并存入凭据的初始版本。

您需要指定凭据名称、初始版本的凭据值和版本号。初始版本的状态被标记为**ACSCurrent**。

您可以指定一个对称密钥类型的用户主密钥作为保护凭据的加密密钥。当不指定CMK时，凭据管家将为您自动创建一个主密钥，用于默认加密您的阿里云账号在本地域创建的凭据。凭据管家加密每个版本的凭据值，凭据名称、版本号、版本的状态标记等元数据不会被加密。

如果您指定主密钥，则需要同时具备相应主密钥的`kms:GenerateDataKey`权限，用于对凭据值进行加密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=CreateSecret&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|CreateSecret|要执行的操作，取值：CreateSecret。 |
|SecretData|String|是|\{"user":"root","passwd":"\*\*\*\*"\}|新创建凭据的凭据值。凭据管家将其加密后，存入初始版本中。 |
|SecretName|String|是|mydbconninfo|凭据名称。 |
|VersionId|String|是|v1|初始版本的版本号。凭据对象内版本号唯一。 |
|EncryptionKeyId|String|否|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|用于加密保护凭据值的KMS主密钥的标识符。

 如果不指定，则凭据管家使用系统创建的密钥来加密保护凭据数据。

 **说明：** KMS主密钥必须是对称密钥。 |
|SecretDataType|String|否|text|凭据值类型。取值：

 -   text
-   binary |
|Description|String|否|mydbinfo|凭据的描述信息。 |
|Tags|String|否|\[\{\\"TagKey\\":\\"key1\\",\\"TagValue\\":\\"val1\\"\},\{\\"TagKey\\":\\"key2\\",\\"TagValue\\":\\"val2\\"\}\]|凭据的标签。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|Arn|String|acs:kms:test-1:127046163668\*\*\*\*:secret/seret001|阿里云资源名称。 |
|RequestId|String|2c124f6f-4210-499f-b88a-69f54004d2d8|请求ID。 |
|SecretName|String|mydbconninfo|凭证名称。 |
|VersionId|String|v1|幂等操作版本号。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=CreateSecret
&SecretData={"user":"root","passwd":"****"}
&SecretDataType=text
&SecretName=mydbconninfo
&VersionId=v1
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
		  <Arn>acs:kms:test-1:127046163668****:secret/secret001</Arn>
		  <SecretName>mydbconninfo</SecretName>
		  <VersionId>v1</VersionId>
		  <RequestId>2c124f6f-4210-499f-b88a-69f54004d2d8</RequestId>
</KMS>
```

`JSON` 格式

```
{
	"Arn": "acs:kms:test-1:127046163668****:secret/secret001",
	"SecretName": "mydbconninfo",
	"VersionId": "v1",
	"RequestId": "2c124f6f-4210-499f-b88a-69f54004d2d8"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

