# DeleteKeyMaterial

调用DeleteKeyMaterial接口删除已导入的密钥材料。

此操作不会删除密钥材料对应的主密钥（CMK）。

如果主密钥处于待删除状态，删除密钥材料不会改变密钥状态和预计删除时间；如果主密钥不处于待删除状态，删除密钥材料会使得密钥状态变更为等待导入。

删除密钥材料后，您可以重新导入密钥材料，但必须与之前的密钥材料相同。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DeleteKeyMaterial&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DeleteKeyMaterial|要执行的操作，取值：DeleteKeyMaterial。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|密钥ID。主密钥（CMK）的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteKeyMaterial
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
    <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

`JSON` 格式

```
{
        "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

## 错误码

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

