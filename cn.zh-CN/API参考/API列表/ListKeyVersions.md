# ListKeyVersions {#concept_1926028 .concept}

列出主密钥的所有密钥版本。

## 请求参数 {#section_g87_jfv_6z4 .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|主密钥的全局唯一标识符|
|PageSize|Integer|否|每页返回的结果个数。参数值为0~101之间的整数。默认值为10。|
|PageNumber|Integer|否|当前页数。 参数值为大于0的整数，默认值为1。|

## 返回参数 {#section_6g6_6y4_3x3 .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID|
|PageSize|Integer|每页的返回结果个数|
|PageNumber|Integer|当前页数|
|TotalCount|Integer|返回的密钥版本总数|
|KeyVersions|[KeyVersion](intl.zh-CN/API 参考/API列表/DescribeKeyVersion.md#section_qvb_ed3_i6n)的数组|返回的密钥版本数组|

## 示例 {#section_37n_20u_pdr .section}

请求示例

``` {#codeblock_6kd_f4l_4cf}
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListKeyVersions
&KeyId=<key id>
&PageNumber=1
&PageSize=10
&<其他公共参数>
```

返回示例

`JSON`格式

``` {#codeblock_hx2_lnm_bu0}
//json response
{
        "RequestId": "1e76f572-4a9b-4be2-a296-ae3069318070",
        "KeyVersions": {
                "KeyVersion": [
                        {
                                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c440b",
                                "KeyVersionId": "1e3304fd-68ac-4d5b-8886-ae5f01a1af61",
                                "CreationDate": "2019-08-06T10:22:03Z"
                        },
                        {
                                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c440b",
                                "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8ecf3",
                                "CreationDate": "2019-08-06T10:19:18Z"
                        },
                        {
                                "KeyId": "0b30658a-ed1a-4922-b8f7-a673ca9c440b",
                                "KeyVersionId": "6a69c763-388a-4708-9fc0-4322266bf2d0",
                                "CreationDate": "2019-08-06T10:17:04Z"
                        }
                ]
        },
        "TotalCount": 3,
        "PageNumber": 1,
        "PageSize": 10
}
```

`XML`格式

``` {#codeblock_76o_ynt_dh1}
//xml response
<KMS>
        <RequestId>f71204c4-53cd-4eea-b405-653ba2db7e86</RequestId>
        <KeyVersions>
                <KeyVersion>
                        <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c440b</KeyId>
                        <KeyVersionId>1e3304fd-68ac-4d5b-8886-ae5f01a1af61</KeyVersionId>
                        <CreationDate>2019-08-06T10:22:03Z</CreationDate>
                </KeyVersion>
                <KeyVersion>
                        <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c440b</KeyId>
                        <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8ecf3</KeyVersionId>
                        <CreationDate>2019-08-06T10:19:18Z</CreationDate>
                </KeyVersion>
                <KeyVersion>
                        <KeyId>0b30658a-ed1a-4922-b8f7-a673ca9c440b</KeyId>
                        <KeyVersionId>6a69c763-388a-4708-9fc0-4322266bf2d0</KeyVersionId>
                        <CreationDate>2019-08-06T10:17:04Z</CreationDate>
                </KeyVersion>
        </KeyVersions>
        <TotalCount>3</TotalCount>
        <PageNumber>1</PageNumber>
        <PageSize>10</PageSize>
</KMS>
```

