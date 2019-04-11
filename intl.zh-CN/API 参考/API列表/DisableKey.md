# DisableKey {#concept_35151_zh .concept}

将一个指定的主密钥（CMK）标记为禁用状态。处于禁用状态的 CMK 无法用于加密、解密操作；恢复至启用状态之前，原来使用该 CMK 加密的密文也无法解密。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK 的全局唯一标识符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的 ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DisableKey
&KeyId=<cmkid>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
"RequestId": "2fe70ce2-3303-4fd6-b3ac-472fb2705c62"
}

```

 `XML` 格式

```
//xml response
<KMS>
    <RequestId>2fe70ce2-3303-4fd6-b3ac-472fb2705c62</RequestId>
</KMS>

```

