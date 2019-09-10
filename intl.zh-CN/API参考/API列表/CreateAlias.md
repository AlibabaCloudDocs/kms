# CreateAlias {#concept_68624_zh .concept}

给主密钥（CMK）创建一个别名。

**说明：** 

-   每个别名只能表示一个 CMK。
-   在同一用户的一个地区内，别名不可重复。
-   可以使用 [UpdateAlias](cn.zh-CN/API 参考/API列表/UpdateAlias.md#) 更新别名和主密钥的映射关系。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|AliasName|String|是|- CMK 的别名，可以使用别名调用 `Encrypt`、`GenerateDataKey`、 `DescribeKey`。- 前缀以外的字符长度：最小长度为 1 字符，最大长度为255 字符。 - 必须包含前缀 `alias/`。|
|KeyId|String|是|key的全局唯一标识符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreareAlias
&KeyId=<cmkid>
&AliasName=<alias/example>
&<公共请求参数>

```

**返回示例**

`JSON` 格式

```
//json response
{
    "RequestId": "53790170-1096-4ed2-9c3a-244d75c8740a"
}

```

 `XML` 格式

```
//xml response
<KMS>
    <RequestId>53790170-1096-4ed2-9c3a-244d75c8740a</RequestId>
</KMS>

```

