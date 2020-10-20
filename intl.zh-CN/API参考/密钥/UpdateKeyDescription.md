# UpdateKeyDescription

调用UpdateKeyDescription接口更新主密钥的描述信息。

将主密钥（CMK）的描述信息（[DescribeKey](~~28952~~)接口中的Description属性）替换为用户传入的值。使用此API可以对密钥的描述信息进行添加、变更、删除操作。

## 调试

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Kms&api=UpdateKeyDescription&type=RPC&version=2016-01-20)

## 请求参数

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|UpdateKeyDescription|要执行的操作，取值：UpdateKeyDescription。 |
|Description|String|是|key description example|主密钥的描述性信息。通常用于描述主密钥的用途，例如主密钥保护的数据类型、可使用主密钥的应用等。 |
|KeyId|String|是|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|密钥ID。主密钥的全局唯一标识符。 |

## 返回数据

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|请求ID。 |

## 示例

请求示例

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateKeyDescription
&Description=key description example
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
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

访问[错误中心](https://error-center.alibabacloud.com/status/product/Kms)查看更多错误码。

