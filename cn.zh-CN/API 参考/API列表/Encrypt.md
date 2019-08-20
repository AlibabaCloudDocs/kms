# Encrypt {#concept_28949_zh .concept}

通过使用主密钥（CMK）将明文加密为密文。

-   可以加密最多为 6KB 任意数据，比如 RSA 密钥，数据库密码，或其他的敏感信息。
-   如果您是从一个 region 迁移加密数据到另一个 region，可以使用这个 API 在新的 region 中加密从另一个 region 中转移过来的明文 DataKey。新 region 里会生成一个加密后的 DataKey。你可以在新 region 将其[Decrypt](cn.zh-CN/API 参考/API列表/Decrypt.md#)。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符。该 API 支持使用别名，详情见[别名使用说明](../../../../../cn.zh-CN/用户指南/别名使用说明.md#)。|
|Plaintext|String|是|待加密明文（必须经过 Base64 编码）。|
|EncryptionContext|String to string map|否|key/value对的 JSON字符串，如果指定了该参数，则在调用`Decrypt` 时需要提供同样的参数，参见[EncryptionContext说明](../../../../../cn.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 { .section}

|名称|类型|描述|
|KeyId|String|CMK 的全局唯一标识符。如果请求使用的别名，此处返回的是别名对应的主密钥 ID。|
|CiphertextBlob|String|加密过的密文。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=Encrypt
&KeyId=<cmkid or aliasname>
&Plaintext=<data need encrypt>
&EncryptionContext={"Example":"Example"}
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
	"KeyId": "your-key-id",
	"CiphertextBlob": "CiphertextBlob",
	"RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}

```

 `XML` 格式

```
//xml response
<KMS>
	<KeyId>your-key-id</KeyId>
	<CiphertextBlob>CiphertextBlob</CiphertextBlob>
	<RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>


```

