# GenerateDataKeyWithoutPlaintext {#concept_1941891 .concept}

生成一个随机的数据密钥，您可以用数据密钥进行本地数据的加密。

此API随机生成一个数据密钥，并通过您指定的主密钥（CMK）加密后，返回数据密钥的密文。此API和[GenerateDataKey](intl.zh-CN/API 参考/API列表/GenerateDataKey.md#)提供完全相同的功能，唯一的区别是此API不会返回数据密钥的明文。

与[GenerateDataKey](intl.zh-CN/API 参考/API列表/GenerateDataKey.md#)一样，您在请求中指定的CMK，仅会被用作数据密钥的加密，和数据密钥的生成没有关系。KMS也不会记录或存储随机生成的数据密钥，您需要负责对数据密钥（密文）进行持久化。

**说明：** 

此API适用于不需要立即使用数据密钥完成数据加密的系统。在系统需要加密的时候，再通过调用[Decrypt](intl.zh-CN/API 参考/API列表/Decrypt.md#) API解开数据密钥的密文。

此API也适用于具有不同信任等级的分布式系统。例如，您的系统将数据按照既定划分策略存储到不同的分区中。其中的一个模块会预先创建不同的数据分区，对每一个分区分别产生不同的数据密钥。这一模块完成控制平面的初始化之后，并不参与数据的生产和消费，它是密钥分发者。而数据平面的模块，在产生和消费数据的时候，首先获取分区的数据密钥密文，在解开之后使用数据密钥的明文对数据执行加密或者解密操作，随后清除内存中的数据密钥明文。在这样的系统中，密钥分发者不需要获取到数据密钥的明文，只需要使用相关CMK的`GenerateDataKeyWithoutPlaintext`的权限；而数据的生产和消费者，不需要产生新的数据密钥，只需要使用相关CMK的`Decrypt`的权限。

## 请求参数 {#section_99u_819_1t9 .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥（CMK）的全局唯一标识符。该参数也可以被指定为CMK绑定的别名，详情请参见[别名使用说明](../../../../intl.zh-CN/用户指南/别名使用说明.md#)。|
|KeySpec|String|否|指定生成的数据密钥的长度。AES\_256表示256比特的对称密钥，AES\_128表示128比特的对称密钥。 有效值：AES\_256或AES\_128。

 **说明：** 

建议使用`KeySpec`或者`NumberOfBytes`（两者之一）来指定数据密钥长度。

-   如果两者都不指定，KMS生成256比特的数据密钥。
-   如果两者都被指定，KMS会忽略`KeySpec`参数。

 |
|NumberOfBytes|Integer|否|指定生成的数据密钥的长度，以字节为单位。 有效值：1到1024。

 **说明：** 

建议使用`KeySpec`或者`NumberOfBytes`（两者之一）来指定数据密钥长度。

-   如果两者都不指定，KMS生成256比特的数据密钥。
-   如果两者都被指定，KMS会忽略`KeySpec`参数。

 |
|EncryptionContext|String to string map|否|key/value对的json字符串，如果指定了该参数，则在调用`Decrypt` 时需要提供同样的参数，详情请参见[EncryptionContext说明](../../../../intl.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 {#section_g83_axw_90n .section}

|名称|类型|描述|
|KeyId|String|CMK的全局唯一标识符。 **说明：** 如果请求中的KeyId参数使用的是CMK的别名，在响应中会返回别名对应的CMK标志符。

 |
|KeyVersionId|String|用于加密明文的密钥版本标志符。是指定CMK的主版本。|
|CiphertextBlob|String|数据密钥被指定CMK的主版本加密后的密文。|

## 示例 {#section_n0o_ujt_zqp .section}

请求示例

``` {#codeblock_5lq_orh_2k4}
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=<cmkid or aliasname>
&KeySpec=AES_256
&EncryptionContext={"Example":"Example"}
&<公共请求参数>
```

返回示例

`JSON`格式

``` {#codeblock_1uo_aas_d0i}
//json response
{
        "CiphertextBlob": "CiphertextBlob",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8ecf3",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}   
```

`XML`格式

``` {#codeblock_mp0_fge_dxo}
//xml response
<KMS>
        <CiphertextBlob>CiphertextBlob</CiphertextBlob>
        <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
        <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8ecf3</KeyVersionId>
        <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
```

