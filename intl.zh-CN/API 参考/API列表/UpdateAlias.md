# UpdateAlias {#concept_68625_zh .concept}

更新已存在的别名所代表的主密钥（CMK）。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|AliasName|String|是|要操作的别名。1.  必须包含前缀`alias/`。
2.  不包含前缀的字符长度为 \[1, 255\]。

|
|KeyId|String|是|CMK 的全局唯一标识符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=UpdateAlias
&AliasName=<alias name>
&KeyId=<target keyid>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "RequestId": "1d2baaf3-d357-46c2-832e-13560c2bd9cd"
}

```

 `XML` 格式

```
//xml response
<KMS>
        <RequestId>1d2baaf3-d357-46c2-832e-13560c2bd9cd</RequestId>
</KMS>

```

