# Encrypt {#concept_28949_zh .concept}

通过使用主密钥（CMK）将明文加密为密文。

-   KMS使用指定CMK的主版本对传入数据进行加密。
-   可以加密最多为6KB任意数据，例如RSA密钥、数据库密码或其它的敏感信息。
-   如果您是从一个region迁移加密数据到另一个region，可以使用这个API在新的region中加密从另一个region中转移过来的明文DataKey。新region里会生成一个加密后的DataKey。您可以在新region将其[Decrypt](intl.zh-CN/API 参考/API列表/Decrypt.md#)。

## 请求参数 {#section_18d_shr_wc7 .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符。该参数也可以被指定为CMK绑定的别名，详情请参见[别名使用说明](../../../../intl.zh-CN/用户指南/别名使用说明.md#)。|
|Plaintext|String|是|待加密明文（必须经过Base64编码）。|
|EncryptionContext|String to string map|否|key/value的JSON字符串。如果指定了该参数，则在调用`Decrypt`时需要提供同样的参数，详情请参见[EncryptionContext说明](../../../../intl.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 {#section_vmh_oql_lb2 .section}

|名称|类型|描述|
|KeyId|String|CMK的全局唯一标识符。 **说明：** 如果请求中的KeyId参数使用的是CMK的别名，在响应中会返回别名对应的CMK标志符。

 |
|KeyVersionId|String|用于加密明文的密钥版本标志符。是指定CMK的主版本。|
|CiphertextBlob|String|数据被指定CMK的主版本加密后的密文。|
|RequestId|String|当前请求的标志符。|

## 示例 {#section_fu7_54r_527 .section}

请标志符求示例

``` {#codeblock_qyd_j81_mbe}
https://kms.cn-hangzhou.aliyuncs.com/?Action=Encrypt
&KeyId=<cmkid or aliasname>
&Plaintext=<data need encrypt>
&EncryptionContext={"Example":"Example"}
&<公共请求参数>
```

返回示例

`JSON`格式

``` {#codeblock_vmc_k9o_4j3}
//json response
{
    "KeyId": "your-key-id",
    "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8ecf3",
    "CiphertextBlob": "CiphertextBlob",
    "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}     
```

`XML`格式

``` {#codeblock_859_7uo_id7}
//xml response
<KMS>
    <KeyId>your-key-id</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8ecf3</KeyVersionId>
    <CiphertextBlob>CiphertextBlob</CiphertextBlob>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>   
```

