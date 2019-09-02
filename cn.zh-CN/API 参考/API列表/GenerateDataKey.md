# GenerateDataKey {#concept_28948_zh .concept}

生成一个随机的数据密钥，您可以用数据密钥进行本地数据的加密。

此API随机生成一个数据密钥，并通过您指定的主密钥（CMK）加密后，返回数据密钥的密文和明文。您可以使用返回的数据密钥明文，在KMS之外对数据进行本地离线加密；您在存储被加密后的数据时，也需要存储数据密钥的密文。您可以通过响应中的`Plaintext`字段获取到数据密钥的明文，通过`CiphertextBlob`字段获取到数据密钥的密文。

您在请求中指定的CMK，仅会被用作数据密钥的加密，和数据密钥的生成没有关系。KMS也不会记录或存储随机生成的数据密钥，您需要负责对数据密钥（密文）进行持久化。

**说明：** 

建议您使用以下方式在本地进行数据加密：

-   调用GenerateDataKey API，获得数据加密密钥。
-   使用数据密钥的明文（通过响应中的`Plaintext`字段返回），在本地完成离线数据加密，随后清除内存中的数据密钥明文。
-   将数据密钥的密文（通过响应中的`CiphertextBlob`字段返回），和本地离线加密后的数据一并进行存储。

在本地解密数据：

-   调用[Decrypt](intl.zh-CN/API 参考/API列表/Decrypt.md#) API解密本地存储的数据密钥的密文。这一操作将返回数据密钥的明文。
-   使用数据密钥的明文，在本地完成离线数据解密，随后清除内存中的数据密钥明文。

## 请求参数 {#section_eoc_mnj_akv .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符。该参数也可以被指定为CMK绑定的别名，详情见[别名使用说明](../../../../intl.zh-CN/用户指南/别名使用说明.md#)。|
|KeySpec|String|否|指定生成的数据密钥的长度。AES\_256表示256比特的对称密钥，AES\_128表示128比特的对称密钥。 有效值：AES\_256、AES\_128。

 **说明：** 

建议使用KeySpec或者NumberOfBytes（两者之一）来指定数据密钥长度。

-   如果两者都不指定，KMS生成256比特的数据密钥。
-   如果两者都被指定，KMS会忽略KeySpec参数。

 |
|NumberOfBytes|Integer|否|指定生成的数据密钥的长度，以字节为单位。 有效值：1~1024。

 **说明：** 

建议使用KeySpec或者NumberOfBytes（两者之一）来指定数据密钥长度。

-   如果两者都不指定，KMS生成256比特的数据密钥。
-   如果两者都被指定，KMS会忽略KeySpec参数。

 |
|EncryptionContext|String to string map|否|key/value对的JSON字符串。如果指定了该参数，则在调用Decrypt时需要提供同样的参数，详情请参见[EncryptionContext说明](../../../../intl.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 {#section_nui_99p_cr1 .section}

|名称|类型|描述|
|KeyId|String|CMK的全局唯一标识符。 **说明：** 如果请求中的KeyId参数使用的是CMK的别名，在响应中会返回别名对应的CMK标志符。

 |
|KeyVersionId|String|用于加密明文的密钥版本标志符。是指定CMK的主版本。|
|Plaintext|String|数据密钥的明文经过Base64编码的后的值。|
|CiphertextBlob|String|数据密钥被指定CMK的主版本加密后的密文。|

## 示例 {#section_0up_l2r_ecs .section}

请求示例

``` {#codeblock_ouj_lcb_nbp}
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=<cmkid or aliasname>
&KeySpec=AES_256
&EncryptionContext={"Example":"Example"}
&<公共请求参数>     
```

返回示例

`JSON`格式

``` {#codeblock_7ca_isv_jh1}
//json response
{
        "CiphertextBlob": "CiphertextBlob",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8ecf3",
        "Plaintext": "Base64 encoded plaintext",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
} 
```

`XML`格式

``` {#codeblock_vra_v3u_lwi}
//xml response
<KMS>
        <CiphertextBlob>CiphertextBlob</CiphertextBlob>
        <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
        <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8ecf3</KeyVersionId>
        <Plaintext>Base64 encoded plaintext</Plaintext>
        <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
```

