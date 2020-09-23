# EnableKey

调用EnableKey接口启用指定的主密钥进行加解密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=EnableKey&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|EnableKey|要执行的操作，取值：EnableKey。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|密钥ID。主密钥的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|efb1cbbd-a093-4278-bc03-639dd4fcc207|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=EnableKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
      <RequestId>efb1cbbd-a093-4278-bc03-639dd4fcc207</RequestId>
</KMS>
```

`JSON` 格式

```
{
"RequestId": "efb1cbbd-a093-4278-bc03-639dd4fcc207"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

