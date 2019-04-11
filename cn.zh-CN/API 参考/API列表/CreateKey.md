# CreateKey {#concept_28947_zh .concept}

创建一个主密钥。

主密钥可以直接用来加密少量的数据（少于6KB），但通常用来生成可以加密大量数据的DataKey，请参见[GenerateDataKey](cn.zh-CN/API 参考/API列表/GenerateDataKey.md#) 。

## 请求参数 {#section_28947_01 .section}

|名称|类型|是否必需|描述|
|Origin|String|否|密钥材料来源。有效值：Aliyun\_KMS或 EXTERNAL。

**说明：** 有效值默认为Aliyun\_KMS。请注意区分大小写。

如果选择 EXTERNAL，您需要[导入密钥材料](../../../../../cn.zh-CN/用户指南/导入密钥材料.md#)。|
|Description|String|否|密钥的描述。 长度必须在 0 到 8192 个字符之间。|
|KeyUsage|String|否|密钥的用途。默认值：ENCRYPT/DECRYPT。|

## 返回参数 {#section_28947_02 .section}

|名称|类型|描述|
|KeyMetadata|[KeyMetadata](#section_28947_03)|密钥的 metadata。|

## KeyMetadata {#section_28947_03 .section}

|名称|类型|描述|
|CreationDate|Timestamp|创建密钥时的日期和时间（UTC时间）。|
|Description|String|密钥的描述。|
|KeyId|String|密钥的全局唯一标识符。|
|KeyState|String|密钥的状态。详情请参见[用户主密钥（CMK）的状态（KeyState）对API调用的影响](cn.zh-CN/API 参考/用户主密钥（CMK）的状态（KeyState）对API调用的影响.md#) 。|
|KeyUsage|String|密钥的用途，加密/解密。|
|DeleteDate|Timestamp|密钥预计被删除的时间（UTC时间）。-   当该值为空时，表示密钥不会被删除。
-   只有当`KeyState`是**PendingDeletion**时，会返回这个参数。

|
|Creator|String|密钥的创建者。|
|Arn|String|当前密钥的阿里云资源名称。|
|Origin|String|密钥材料来源。|
|MaterialExpireTime|String|密钥材料过期时间（UTC时间）。当该值为空时，表示密钥材料不会过期。|

## 示例 {#section_28947_04 .section}

**请求示例**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&Description=<your key description>
&KeyUsage=ENCRYPT/DECRYPT
&Origin=<key origin, default Aliyun_KMS>
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
                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
                "KeyState": "Enabled",
                "KeyUsage": "ENCRYPT/DECRYPT",
                "DeleteDate": "",
                "Creator":"123456",
                "Arn":"acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
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
        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</KeyId>
        <KeyState>Enabled</KeyState>
        <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
        <DeleteDate></DeleteDate>
        <Creator>123456</Creator>
        <Arn>acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</Arn>
        <Origin>Aliyun_KMS</Origin>
        <MaterialExpireTime></MaterialExpireTime>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>


```

