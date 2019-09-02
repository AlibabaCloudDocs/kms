# CreateKeyVersion {#concept_1925932 .concept}

为主密钥创建一个新的密钥版本。

此API会创建一个新的密钥版本，并且设置其为主版本。下列情况不允许创建新的密钥版本：

-   指定的主密钥为云产品托管的默认密钥。
-   指定的主密钥为用户自带密钥（外部导入到KMS的密钥）。
-   指定的主密钥处于Enabled之外的状态。

## 请求参数 {#section_0id_nci_k0r .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥的全局唯一标识符|

## 返回参数 {#section_saj_x43_6is .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID|
|KeyVersion|[KeyVersion](intl.zh-CN/API 参考/API列表/DescribeKeyVersion.md#section_qvb_ed3_i6n)|新创建密钥版本的元数据|

## 示例 {#section_ozr_bt0_5pt .section}

请求示例

``` {#codeblock_h72_xna_ctx}
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreareKeyVersion
&KeyId=<cmkid>
&<公共请求参数>
			
```

返回示例

`JSON` 格式

``` {#codeblock_sg4_0dc_4yi}
//json response
{
        "KeyVersion": {
                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c440b",
                "KeyVersionId": "6a69c763-388a-4708-9fc0-4322266bf2d0",
                "CreationDate": "2019-08-06T10:17:04Z"
        },
        "RequestId": "80b4eac8-9f51-452a-a859-0c9b06b283c1"
}
```

`XML` 格式

``` {#codeblock_oz8_xxr_bbo}
//xml response
<KMS>
        <KeyVersion>
                <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c440b</KeyId>
                <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8ecf3</KeyVersionId>
                <CreationDate>2019-08-06T10:19:18Z</CreationDate>
        </KeyVersion>
        <RequestId>b0ae52a2-33a4-43de-b68c-849f81d09f5d</RequestId>
</KMS>
```

