# EnableKey {#concept_35150_zh .concept}

将一个指定的 CMK 标记为启用状态，可以使用它进行加解密。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|string|是|CMK 的全局唯一标识符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次 API 请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=EnableKey
&KeyId=<cmkid>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
"RequestId": "efb1cbbd-a093-4278-bc03-639dd4fcc207"
}

```

 `XML` 格式

```
//xml response

<KMS>
    <RequestId>efb1cbbd-a093-4278-bc03-639dd4fcc207</RequestId>
</KMS>

```

