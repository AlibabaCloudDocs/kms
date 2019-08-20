# CancelKeyDeletion {#concept_44197_zh .concept}

撤销密钥删除。当密钥删除的申请撤销成功以后，密钥会处于**启用**状态。

## 请求参数 { .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK的全局唯一标示符。|

## 返回参数 { .section}

|名称|类型|描述|
|RequestId|String|本次请求的ID。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CancelKeyDeletion
&KeyId=<cmkid>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
"RequestId": "3da5b8cc-8107-40ac-a170-793cd181d7b7"
}

```

 `XML` 格式

```
//xml response
<KMS>
    <RequestId>3da5b8cc-8107-40ac-a170-793cd181d7b7</RequestId>
</KMS>

```

