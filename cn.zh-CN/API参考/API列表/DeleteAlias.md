# DeleteAlias {#concept_68626_zh .concept}

删除别名。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|AliasName|String|是|要操作的别名。-   必须包含前缀`alias/`。
-   不包含前缀的字符长度为 \[1, 255\]。

|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DeleteAlias
&AliasName=<alias name>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "RequestId": "4c8ae23f-3a42-6791-a      4ba-1faa77831c28"
}

```

 `XML` 格式

```
//xml response
<KMS>
        <RequestId>4c8ae23f-3a42-6791-a 4ba-1faa77831c28</RequestId>
</KMS>

```

