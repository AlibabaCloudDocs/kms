# GenerateDataKey {#concept_28948_zh .concept}

生成一个密钥，你可以用这个密钥进行本地数据的加密。

这个 API 在`Plaintext`字段返回一个明文密钥，在`CiphertextBlob`字段返回一个加密后的密钥。

**说明：** 

-   我们建议您使用以下方式在本地进行数据加密：
    -   调用本文 API `GenerateDataKey`，获得数据加密密钥。
    -   在返回结果中，使用`Plaintext`中的明文密钥对本地加密数据，然后删除内存中的明文密钥。
    -   在本地存储`CiphertextBlob`中返回的加密过的密钥，和加密后的数据。
-   在本地解密数据：
    -   调用[Decrypt](intl.zh-CN/API 参考/API列表/Decrypt.md#)，将`CiphertextBlob`返回的加密过的密钥，解密为`Plaintext`密钥。
    -   用`Plaintext`密钥为本地数据解密，再删除本地存储中的`Plaintext`密钥。
-   当`KeySpec`和`NumberOfBytes`都不填写时，默认`KeySpec`为AES\_256。
-   同时指定`NumberOfBytes`和`KeySpec`时，以`NumberOfBytes`为准。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符。该 API 支持使用别名，详情见[别名使用说明](../../../../intl.zh-CN/用户指南/别名使用说明.md#)。|
|KeySpec|String|否|产生数据密钥的长度与类型，AES\_256表示256 比特的对称密钥，AES\_128表示 128 比特的对称密钥。|
|NumberOfBytes|Integer|否|产生数据密钥的长度，以字节为单位。有效值：1 到 1024。|
|EncryptionContext|String to string map|否|key/value对的json字符串，如果指定了该参数，则在调用`Decrypt` 时需要提供同样的参数，参见[EncryptionContext说明](../../../../intl.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 { .section}

|名称|类型|描述|
|KeyId|String|CMK 的全局唯一标识符。如果请求使用的别名，此处返回的是别名对应的主密钥 ID。|
|Plaintext|String|明文 data key，该 data key 是经过 base64 编码的。|
|CiphertextBlob|String|加密过的 data key。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=<cmkid or aliasname>
&KeySpec=AES_256
&EncryptionContext={"Example":"Example"}
&<公共请求参数>
			
```

**返回示例**

`JSON` 格式

```
//json response
{
        "CiphertextBlob": "CiphertextBlob",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "Plaintext": "Base64 encoded plaintext",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}

			
```

`XML` 格式

```
//xml response
<KMS>
        <CiphertextBlob>CiphertextBlob</CiphertextBlob>
        <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
        <Plaintext>Base64 encoded plaintext</Plaintext>
        <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
			
```

