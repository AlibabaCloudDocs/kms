# DisableKey

调用DisableKey接口禁用指定的主密钥（CMK）进行加解密。

恢复至启用状态之前，原来使用该主密钥加密的密文无法解密。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=DisableKey&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DisableKey|要执行的操作，取值：DisableKey。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|密钥ID。主密钥的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|2fe70ce2-3303-4fd6-b3ac-472fb2705c62|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DisableKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<公共请求参数>
```

正常返回示例

`XML` 格式

```
<KMS>
      <RequestId>2fe70ce2-3303-4fd6-b3ac-472fb2705c62</RequestId>
</KMS>
```

`JSON` 格式

```
{
	"RequestId": "2fe70ce2-3303-4fd6-b3ac-472fb2705c62"
}
```

## 错误码

访问[错误中心](https://error-center.aliyun.com/status/product/Kms)查看更多错误码。

