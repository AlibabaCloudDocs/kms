# TagResource {#reference_303902 .reference}

为用户主密钥添加或修改标签。

## 描述 {#section_lm7_4hv_cnd .section}

每个用户主密钥可以有多个标签，一个标签由一组标签键和标签值进行定义。

**说明：** 每个用户主密钥最多可以添加 10 个标签。

关于标签键和标签值，详情请参考：[Tag 对象说明](#section_ut1_vco_umg)。

## 请求格式 {#section_dr8_4wg_yvi .section}

``` {#codeblock_fiz_ezz_b58}
KeyId="string"&Tags=[{ "TagKey": "string","TagValue": "string"} ]
```

## 请求参数 {#section_wsc_ki3_fc2 .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|KeyId|String|是|external key id|全局唯一标识符。|
|Tags|JSON|是|\[\{"TagKey": "Project", "TagValue": "Test"\}\]| 一个或者多个标签。格式为：Tag 对象数组，其中 Tag 对象有下列属性：

 -   TagKey：标签的标签键。
-   TagValue：标签的标签值。

 关于标签键和标签值，详情请参考：[Tag 对象说明](#section_ut1_vco_umg)。

 |

## Tag 对象说明 {#section_ut1_vco_umg .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|TagKey|String|是|Project| 标签的标签键。

 长度范围： 1~128 字符。

 字符限制：`a-zA-Z0-9/_-.+=@:`

 |
|TagValue|String|是|Test| 标签的标签值。

 长度范围： 0~256 字符。

 字符限制：`a-zA-Z0-9/_-.+=@:`

 **说明：** 每个标签的标签键互不相同。调用 TagResource 接口时，如果输入的标签键在指定密钥上已经存在，则使用输入的标签值覆盖原标签值。

 |

## 请求示例 {#section_1w3_d5i_l5l .section}

``` {#codeblock_v84_yv4_whg}
https://kms.cn-hangzhou.aliyuncs.com/?Action=TagResource
&KeyId=<external key id>
&Tags=<tags>
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

