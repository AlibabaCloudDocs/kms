# SetDeletionProtection

调用SetDeletionProtection接口为用户主密钥（CMK）开启或关闭删除保护。

使用说明：

-   当您为CMK开启删除保护后，将无法删除该CMK。如果需要删除CMK，需提前关闭删除保护。
-   调用SetDeletionProtection接口前，请确保CMK不处于待删除状态。您可以调用[DescribeKey](~~28952~~)接口查看CMK的状态（KeyState）。

本文将提供一个示例，为CMK ARN（ProtectedResourceArn）为`acs:kms:cn-hangzhou:123213123****:key/0225f411-b21d-46d1-be5b-93931c82****`的CMK开启删除保护。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=SetDeletionProtection&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|SetDeletionProtection|要执行的操作，取值：SetDeletionProtection。 |
|EnableDeletionProtection|Boolean|是|true|是否开启删除保护，取值：

 -   true：开启删除保护。
-   false（默认值）：关闭删除保护。 |
|ProtectedResourceArn|String|是|acs:kms:cn-hangzhou:123213123\*\*\*\*:key/0225f411-b21d-46d1-be5b-93931c82\*\*\*\*|待设置删除保护的CMK ARN。

 您可以调用[DescribeKey](~~28952~~)接口查看CMK ARN（Arn）。 |
|DeletionProtectionDescription|String|否|该密钥正在被XXX服务使用。已为您设置删除保护。|删除保护描述。

 **说明：** 当EnableDeletionProtection取值为true时该参数有效。 |

关于公共请求参数的详情，请参见[公共参数](~~69007~~)。

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|请求ID。 |

## 示例

请求示例

```
http(s)://[Endpoint]/?Action=SetDeletionProtection
&EnableDeletionProtection=true
&ProtectedResourceArn=acs:kms:cn-hangzhou:123213123****:key/0225f411-b21d-46d1-be5b-93931c82****
&<公共请求参数>
```

正常返回示例

`XML`格式

```
<KMS>
      <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON`格式

```
{
    "RequestId":"3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

