# ListResourceTags {#reference_303904 .reference}

列出用户主密钥的标签。

## 请求格式 {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"
```

## 请求参数 {#section_wsc_ki3_fc2 .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|KeyId|String|是|key id|全局唯一标识符。|

## 请求示例 {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=ListResourceTags
&KeyId=<key id>
&<其他公共参数>
```

## 返回参数 {#section_1mx_9zy_w2g .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|请求 ID。|
|TagKey|String|Project|标签键。|
|TagValue|String|Test|标签值。|

## 返回示例 {#section_pj4_dkc_jiy .section}

JSON 格式

``` {#codeblock_6iw_t7q_e42}
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8",
    "Tags": {
            "Tag": [
                {
                    "KeyId": "33caea95-c3e5-4b3e-a9c6-cec76e4eaf83",
                    "TagKey": "Project",
                    "TagValue": "Test"
                }
            ]
        }
}
```

XML 格式

``` {#codeblock_xis_t6p_fgx}
<KMS>
        <RequestId>0f900dad-c747-4170-9962-1bfb6b31436b</RequestId>
        <Tags>
            <Tag>
                <KeyId>33caea95-c3e5-4b3e-a9c6-cec76e4eaf83</KeyId>
                <TagKey>Project</TagKey>
                <TagValue>Test</TagValue>
            </Tag>
        </Tags>
</KMS>
```

