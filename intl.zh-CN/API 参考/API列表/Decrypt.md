# Decrypt {#concept_28950_zh .concept}

解密CiphertextBlob中的密文。

密文可以是以下API生成的：

-   [GenerateDataKey](intl.zh-CN/API 参考/API列表/GenerateDataKey.md#)
-   [Encrypt](intl.zh-CN/API 参考/API列表/Encrypt.md#)

## 请求参数 {#section_f57_vcb_54s .section}

|名称|类型|是否必需|描述|
|CiphertextBlob|String|是|待解密的密文|
|EncryptionContext|String|否|key/value的JSON字符串。如果在Encrypt或者GenerateDataKey API中指定了该参数，则需要提供同样的参数才能解密，详情请参见[EncryptionContext说明](../../../../intl.zh-CN/用户指南/EncryptionContext说明.md#)。|

## 返回参数 {#section_u6n_gti_k9x .section}

|名称|类型|描述|
|KeyId|String|主密钥的全局唯一标识符。解密密文使用的主密钥CMK ID。|
|KeyVersionId|String|主密钥下用于解密密文的密钥版本标志符。|
|Plaintext|String|解密后的明文。|

## 示例 {#section_5we_k2v_538 .section}

请求示例

``` {#codeblock_z1d_sub_kht}
https://kms.cn-hangzhou.aliyuncs.com/?Action=Decrypt
&CiphertextBlob=<your ciphertextblob>
&EncryptionContext={"Example":"Example"}
&<公共请求参数>     
```

返回示例

`JSON`格式

``` {#codeblock_kct_nr0_uh3}
//json response
{
    "KeyId": "202b9877-5a25-46e3-a763-e20791b5****",
    "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
    "Plaintext": "Plaintext",
    "RequestId": "207596a2-36d3-4840-b1bd-f87044699bd7"
}     
```

`XML`格式

``` {#codeblock_5fj_6ku_npp}
//xml response
<KMS>
        <KeyId>202b9877-5a25-46e3-a763-e20791b5****</KeyId>
        <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
        <Plaintext>Plaintext</Plaintext>
        <RequestId>4bd560a1-729e-45f1-a3d9-b2a33d61046b</RequestId>
</KMS>
```

