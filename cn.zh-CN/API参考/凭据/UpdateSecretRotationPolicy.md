# UpdateSecretRotationPolicy

调用UpdateSecretRotationPolicy接口更新凭据轮转策略。

凭据开启自动轮转后，首次自动轮转的时间为上次轮转时间加上轮转周期。

使用限制：UpdateSecretRotationPolicy接口不支持更新普通凭据的轮转策略。

本文将提供一个示例，更新名称为`RdsSecret/Mysql5.4/MyCred`的凭据轮转策略。具体如下：

-   将`EnableAutomaticRotation`设置为`true`，表示开启自动轮转。
-   将`RotationInterval`设置为`30d`，表示设置轮转周期为30天。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateSecretRotationPolicy&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateSecretRotationPolicy|要执行的操作，取值：UpdateSecretRotationPolicy。 |
|EnableAutomaticRotation|Boolean|是|true|是否开启自动轮转，取值：

 -   true：开启自动轮转。
-   false（默认值）：不开启自动轮转。 |
|SecretName|String|是|RdsSecret/Mysql5.4/MyCred|凭据名称。 |
|RotationInterval|String|否|30d|自动轮转的周期。取值范围：6小时~8,760小时（365天）。

 格式为`integer[unit]`，其中`integer`表示时间长度，`unit`表示时间单位。

 unit取值：d（天）、h（小时）、m（分钟）、s（秒）。例如：7d或者604,800s均表示7天的周期。

 **说明：** 当EnableAutomaticRotation取值为true时，必须设置该参数。反之，将忽略该参数。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|SecretName|String|RdsSecret/Mysql5.4/MyCred|凭据名称。 |
|RequestId|String|2c124f6f-4210-499f-b88a-69f54004d2d8|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=UpdateSecretRotationPolicy
&EnableAutomaticRotation=true
&SecretName=RdsSecret/Mysql5.4/MyCred
&RotationInterval=30d
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
	  <SecretName>RdsSecret/Mysql5.4/MyCred</SecretName>
	  <RequestId>2c124f6f-4210-499f-b88a-69f54004d2d8</RequestId>
</KMS>
```

`JSON`格式

```
{
    "SecretName": "RdsSecret/Mysql5.4/MyCred",
    "RequestId": "2c124f6f-4210-499f-b88a-69f54004d2d8"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

