# DescribeKey {#concept_28952_zh .concept}

返回指定主密钥（CMK）的相关信息。

## 请求参数 {#section_28952_01 .section}

|名称|类型|是否必需|描述|
|KeyId|String|是|CMK 的全局唯一标识符。该 API 支持使用别名，详情见[别名使用说明](../../../../../intl.zh-CN/用户指南/别名使用说明.md#)。|

## 返回参数 {#section_28952_02 .section}

|名称|类型|描述|
|KeyMetadata|[KeyMetadata](#section_28952_03)|CMK 的 metadata。|

## KeyMetadata {#section_28952_03 .section}

|名称|类型|描述|
|CreationDate|Timestamp|创建主密钥（CMK）的日期和时间（UTC）。|
|Description|String|CMK 的描述。|
|KeyId|String|CMK 全局唯一标识符。|
|KeyState|String|CMK 的状态。详情请参见[用户主密钥（CMK）的状态（KeyState）对API调用的影响](intl.zh-CN/API 参考/用户主密钥（CMK）的状态（KeyState）对API调用的影响.md#)。|
|KeyUsage|String|CMK 的用途。|
|DeleteDate|Timestamp|CMK 的预计删除时间。详情请参见[ScheduleKeyDeletion](intl.zh-CN/API 参考/API列表/ScheduleKeyDeletion.md#)。只有`KeyState`为`PendingDeletion`时返回该值。|
|Creator|String|CMK 创建者。|
|Arn|String|阿里云资源名称。|
|Origin|String|CMK 的密钥材料来源。|
|MaterialExpireTime|String|密钥材料过期时间（UTC）。当该值为空时，表示密钥材料不会过期。|

## 示例 { .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeKey
&KeyId=<your-key-id>
&<公共请求参数>

```

**返回示例**

 `JSON` 格式

```
//json response
{
        "KeyMetadata": {
                "CreationDate": "2016-03-25T10:42:40Z",
                "Description": "key description example",
                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddf****",
                "KeyState": "Enabled",
                "KeyUsage": "ENCRYPT/DECRYPT",
                "DeleteDate": "",
                "Creator":"123456",
                "Arn":"acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddf****",
                "Origin":"Aliyun_KMS",
                "MaterialExpireTime":""
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}

```

 `XML` 格式

```
//xml response
<KMS>
 <KeyMetadata>
        <CreationDate>2016-03-25T10:40:47Z</CreationDate>
        <Description>key description example</Description>
        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddf****</KeyId>
        <KeyState>Enabled</KeyState>
        <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
        <DeleteDate></DeleteDate>
        <Creator>123456</Creator>
        <Arn>acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddf****</Arn>
        <Origin>Aliyun_KMS</Origin>
        <MaterialExpireTime></MaterialExpireTime>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>

```

