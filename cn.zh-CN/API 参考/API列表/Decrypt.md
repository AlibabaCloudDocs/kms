# Decrypt {#concept_28950_zh .concept}

解密`CiphertextBlob`中的密文。

密文可以是以下 API 生成的：

-   [GenerateDataKey](cn.zh-CN/API 参考/API列表/GenerateDataKey.md#) 
-    [Encrypt](cn.zh-CN/API 参考/API列表/Encrypt.md#) 

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|CiphertextBlob|String|是|待解密的密文。|
|EncryptionContext|String|否|key/value 对的 JSON字符串，如果在`Encrypt`或者`GenerateDataKey`API 中指定了该参数，则需要提供同样的参数才能解密，参见[EncryptionContext说明](../../../../cn.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 { .section}

|名称|类型|描述|
|KeyId|String|密钥的全局唯一标识符。加密密文使用的主密钥 CMK ID。|
|Plaintext|String|解密后的明文。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=Decrypt
&CiphertextBlob=<your ciphertextblob>
&EncryptionContext={"Example":"Example"}
&<公共请求参数>

```

**返回示例**

`JSON` 格式

```
//json response
{
"KeyId": "202b9877-5a25-46e3-a763-e20791b5****"
"Plaintext": "Plaintext"
"RequestId": "207596a2-36d3-4840-b1bd-f87044699bd7"
}

```

 `XML` 格式

```
//xml response
<KMS>
        <KeyId>202b9877-5a25-46e3-a763-e20791b5****</KeyId>
        <Plaintext>Plaintext</Plaintext>
        <RequestId>4bd560a1-729e-45f1-a3d9-b2a33d61046b</RequestId>
</KMS>


```

