# OpenKmsService

调用OpenKmsService接口为当前阿里云账号开通密钥管理服务。

调用该接口前，请关注：

-   密钥管理服务需要收费，计费详情请参见[计费说明](~~52608~~)。
-   一个阿里云账号只能开通一次。
-   请确保阿里云账号已通过实名认证。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=OpenKmsService&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|OpenKmsService|要执行的操作，取值：OpenKmsService。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=OpenKmsService
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
      <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` 格式

```
{
  "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## 错误码

|HttpCode|错误码|错误信息|描述|
|--------|---|----|--|
|400|CreateLXOrderFailed|Create order failed.|创建订单失败。|
|400|Forbidden.NoRealNameAuthentication|Real name authentication is needed.|未通过实名认证。|
|400|Forbidden.Opened|Your kms service has been opened.|您已开通密钥管理服务。|

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

