# UpdateSecret

调用UpdateSecret接口更新凭据的元数据。

本文将提供一个示例，更新名为`secret001`凭据的元数据，将其描述信息`Description`更新为`datainfo`。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateSecret&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateSecret|要执行的操作，取值：UpdateSecret。 |
|SecretName|String|是|secret001|凭据名称。 |
|Description|String|否|datainfo|凭据的描述信息。 |
|ExtendedConfig.CustomData|Json|否|\{"DBName":"app1","Port":"3306"\}|拓展配置中的自定义数据。

 **说明：**

-   如果指定该参数，将会更新凭据已有的拓展配置。
-   普通凭据不支持设置该参数。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47|请求ID。 |
|SecretName|String|secret001|凭据名称。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateSecret
&Description=datainfo
&SecretName=secret001
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <RequestId>5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47</RequestId>
</KMS>
```

`JSON`格式

```
{
    "SecretName":"secret001",  
    "RequestId": "5b75d8b1-5b6a-4ec0-8e0c-c08befdfad47"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

