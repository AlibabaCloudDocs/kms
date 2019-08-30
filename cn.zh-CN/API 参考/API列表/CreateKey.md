# CreateKey {#concept_28947_zh .concept}

创建一个主密钥。

主密钥可直接用于加密少量数据（少于 6 KB），但通常用于生成可以加密大量数据的 DataKey，详情请参见[GenerateDataKey](intl.zh-CN/API 参考/API列表/GenerateDataKey.md#) 。

## 请求参数 {#section_28947_01 .section}

|名称|类型|是否必需|描述|
|Origin|String|否|密钥材料来源。 有效值：Aliyun\_KMS 或 EXTERNAL。

 **说明：** 

-   有效值默认为 Aliyun\_KMS。请注意区分大小写。
-   如果选择 EXTERNAL，您需要[导入密钥材料](../../../../intl.zh-CN/用户指南/导入密钥材料.md#)。

 |
|Description|String|否|密钥的描述。长度必须在 0 到 8192 个字符之间。|
|KeyUsage|String|否|密钥的用途。 有效值：ENCRYPT/DECRYPT

 默认值：ENCRYPT/DECRYPT。|
|ProtectionLevel|String|否|密钥的保护级别。 有效值：SOFTWARE 或 HSM。

 **说明：** 

默认取值为SOFTWARE。请注意区分大小写。

当指定值为 HSM 时：

-   如果 Origin 为 Aliyun\_KMS，则会在托管密码机中生成密钥，用于执行密码运算。
-   如果 Origin 为 EXTERNAL，您可以将外部密钥导入到托管密码机中，用于执行密码运算。

 |
|EnableAutoRotation|Boolean|否|是否开启自动密钥轮转。 有效值：true 或 false。

 **说明：** 

-   默认取值为 false，即不开启自动轮转。
-   Origin 为 EXTERNAL 时不支持开启自动轮转。

 |
|RotationIntervalInDays|Integer|否|自动轮转周期（天数）。 有效值范围：\[7,730\]

 **说明：** 

-   当 EnableAutoRotation 为 true 时，必须设置此参数。
-   当 EnableAutoRotation 为 false 时，忽略此参数。

 |

## 返回参数 {#section_28947_02 .section}

|名称|类型|描述|
|KeyMetadata|[KeyMetadata](intl.zh-CN/API 参考/API列表/DescribeKey.md#section_28952_03)|密钥的 metadata。|

## 示例 {#section_28947_04 .section}

请求示例

``` {#codeblock_y9t_tq4_gn9}
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&Description=<your key description>
&KeyUsage=ENCRYPT/DECRYPT
&Origin=<key origin, default Aliyun_KMS>
&ProtectionLevel=HSM
&<公共请求参数>
```

返回示例

`JSON` 格式

``` {#codeblock_na5_8jg_hip}
//json response
{
        "KeyMetadata": {
                "CreationDate": "2016-03-25T10:42:40Z",
                "Description": "key description example",
                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
                "KeyState": "Enabled",
                "KeyUsage": "ENCRYPT/DECRYPT",
                "PrimaryKeyVersion": "0ec2d249-9f64-4d8f-9587-1215525e****",
                "DeleteDate": "",
                "Creator":"123456",
                "Arn":"acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****",
                "Origin":"Aliyun_KMS",
                "MaterialExpireTime":"",
                "ProtectionLevel":"HSM",
                "LastRotationDate":"2016-03-25T10:42:40Z",
                "EnableAutoRotation":true,
                "RotationIntervalInDays":365,
                "NextRotationDate":"2017-03-25T10:42:40Z"
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

`XML` 格式

``` {#codeblock_itt_8qv_qm7}
//xml response
<KMS>
 <KeyMetadata>
        <CreationDate>2016-03-25T10:40:47Z</CreationDate>
        <Description>key description example</Description>
        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</KeyId>
        <KeyState>Enabled</KeyState>
        <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
        <PrimaryKeyVersion>0ec2d249-9f64-4d8f-9587-1215525e****</PrimaryKeyVersion>
        <DeleteDate></DeleteDate>
        <Creator>123456</Creator>
        <Arn>acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4****</Arn>
        <Origin>Aliyun_KMS</Origin>
        <MaterialExpireTime></MaterialExpireTime>
        <ProtectionLevel>HSM</ProtectionLevel>
        <LastRotationDate>2016-03-25T10:42:40Z</LastRotationDate>
        <EnableAutoRotation>true</EnableAutoRotation>
        <RotationIntervalInDays>365</RotationIntervalInDays>
        <NextRotationDate>2017-03-25T10:42:40Z</NextRotationDate>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>
```

