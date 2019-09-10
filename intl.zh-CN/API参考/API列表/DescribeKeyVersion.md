# DescribeKeyVersion {#concept_1926001 .concept}

查询指定的密钥版本的元数据信息。

## 请求参数 {#section_597_4oy_q9t .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥的全局唯一标识符|
|KeyVersionId|String|是|密钥版本的标识符|

## 返回参数 {#section_lq8_6um_rkd .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID|
|KeyVersion|[KeyVersion](#section_qvb_ed3_i6n)|密钥版本的元数据|

## KeyVersion {#section_qvb_ed3_i6n .section}

|名称|类型|描述|
|KeyId|String|主密钥的全局唯一标识符|
|KeyVersionId|String|密钥版本的标志符|
|CreationDate|Timestamp|创建密钥版本时的日期和时间（UTC时间）|

## 示例 {#section_nka_s2u_g14 .section}

请求示例

``` {#codeblock_ymx_919_qad}
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeKeyVersion
&KeyId=<cmkid>
&KeyVersionId=<key version id>
&<公共请求参数>
			
```

返回示例

`JSON` 格式

``` {#codeblock_0r1_t7z_ny1}
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

``` {#codeblock_e57_f24_gby}
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

