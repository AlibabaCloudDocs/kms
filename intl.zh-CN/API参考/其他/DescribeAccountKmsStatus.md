# DescribeAccountKmsStatus

调用DescribeAccountKmsStatus接口查询当前阿里云账号的密钥管理服务状态。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DescribeAccountKmsStatus&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeAccountKmsStatus|要执行的操作，取值：DescribeAccountKmsStatus。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|AccountStatus|String|Enabled|当前阿里云账号的密钥管理服务状态，取值：

 -   Enabled：已开通，可正常使用。
-   NotEnabled：未开通。
-   InDebt：已欠费，即将停止服务。

**说明：** 当您的阿里云账号欠费后，请及时续费，以免对您的业务造成影响。

-   Suspended：已停止服务。 |
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=DescribeAccountKmsStatus
```

正常返回示例

`XML` 格式

```
<KMS>
    <AccountStatus>Enabled</AccountStatus>
    <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` 格式

```
{
  "AccountStatus": "Enabled",
  "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

