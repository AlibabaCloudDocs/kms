# UpdateSecretVersionStage

调用UpdateSecretVersionStage接口更新凭据的版本状态。

该接口用于更新凭据的版本状态，支持以下两种操作方式：

-   将指定的版本状态用于标记一个新的凭据版本。
-   将指定的版本状态从被标记的凭据版本上移除。

使用限制：该接口仅支持普通凭据。

本文将提供一个示例，更新名为`secret001`凭据的版本状态，将`ACSCurrent`版本状态用于标记`002`版本。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateSecretVersionStage&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateSecretVersionStage|要执行的操作，取值：UpdateSecretVersionStage。 |
|SecretName|String|是|secret001|凭据名称。 |
|VersionStage|String|是|ACSCurrent|指定版本状态。取值：

 -   ACSCurrent
-   ACSPrevious
-   自定义状态 |
|RemoveFromVersion|String|否|001|将指定的版本状态从此参数指定的版本上移除。

 **说明：** RemoveFromVersion和MoveToVersion至少指定其中一个参数。 |
|MoveToVersion|String|否|002|将指定的版本状态用于标记此参数指定的版本。

 **说明：**

-   RemoveFromVersion和MoveToVersion至少指定其中一个参数。
-   当VersionStage取值为ACSCurrent或ACSPrevious时，必须指定该参数。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|8cad259f-4d77-40ec-bbd7-b9c47a423bb9|请求ID。 |
|SecretName|String|secret001|凭据名称。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateSecretVersionStage
&SecretName=secret001
&VersionStage=ACSCurrent
&MoveToVersion=002
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <RequestId>8cad259f-4d77-40ec-bbd7-b9c47a423bb9</RequestId>  
</KMS>
```

`JSON`格式

```
{
	"SecretName": "secret001",
	"RequestId": "8cad259f-4d77-40ec-bbd7-b9c47a423bb9"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

