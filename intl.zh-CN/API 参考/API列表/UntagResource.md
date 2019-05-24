# UntagResource {#reference_303902 .reference}

删除用户主密钥的指定标签。

## 请求格式 {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"&TagKeys=["tagkey1","tagkey2"]
```

## 请求参数 {#section_wsc_ki3_fc2 .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|KeyId|String|是|external key id|全局唯一标识符。|
|TagsKeys|JSON|是|\["tagkey1","tagkey2"\]|一个或者多个标签键，只需要指定标签键，不需要指定标签值。格式为：String 数组。 数组中的 String 长度范围为：1~128 字符。|

## 请求示例 {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=UntagResource
&KeyId=<external key id>
&TagKeys=<tagkeys>
&<其他公共参数>
```

## 返回参数 {#section_1mx_9zy_w2g .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|RequestId|String|4162a6af-bc99-40b3-a552-89dcc8aaf7c8|请求 ID。|

## 返回示例 {#section_pj4_dkc_jiy .section}

JSON 格式

``` {#codeblock_6iw_t7q_e42}
{
    "RequestId": "4162a6af-bc99-40b3-a552-89dcc8aaf7c8"
}
```

XML 格式

``` {#codeblock_xis_t6p_fgx}
<KMS>
  <RequestId>4162a6af-bc99-40b3-a552-89dcc8aaf7c8</RequestId>
</KMS>
```

