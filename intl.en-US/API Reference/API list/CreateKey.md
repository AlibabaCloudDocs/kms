# CreateKey {#concept_28947_zh .concept}

You can call this operation to create a customer master key \(CMK\).

A CMK is used to directly encrypt a small amout of data \(up to 6 KB of data\). However, it's often used to generate data keys for encrypting a large amount of data. For more information, see [GenerateDataKey](reseller.en-US/API Reference/API list/GenerateDataKey.md#).

## Request parameters {#section_28947_01 .section}

|Parameter|Type|Required|Description|
|Origin|String|No|The source of the key material for the CMK to create. Valid values: Aliyun\_KMS and EXTERNAL.

 **Note:** The default value is Aliyun\_KMS. The value of this parameter is case sensitive.

 If you select EXTERNAL, you must [Import key material](../../../../reseller.en-US/User Guide/Import key material.md#).|
|Description|String|No|The description of the CMK to create. The description must be 0 to 8,192 characters in length.|
|KeyUsage|String|No|The purpose of the CMK to create. Default value: ENCRYPT/DECRYPT|
|ProtectionLevel|String|No|The protection level of the CMK to create. Valid value: SOFTWARE and HSM. When this parameter is set to HSM:

-   If the Origin parameter is set to Aliyun\_KMS, the CMK is created in Managed HSM.
-   If the Origin parameter is set to EXTERNAL, you can import external keys to Managed HSM.

 **Note:** The default value is SOFTWARE. The value of this parameter is case sensitive.

 |

## Response parameters {#section_28947_02 .section}

|Parameter|Type|Description|
|KeyMetadata|[KeyMetadata parameters](#section_28947_03)|The metadata of the CMK created.|

## KeyMetadata parameters {#section_28947_03 .section}

|Parameter|Type|Description|
|CreationDate|Timestamp|The date and time when the CMK was created. The time is displayed in UTC.|
|Description|String|The description of the CMK.|
|KeyId|String|The globally unique ID of the CMK.|
|KeyState|String|The status of the CMK. For more information, see [Impact of CMK states on API call](reseller.en-US/API Reference/Impact of CMK states on API call.md#).|
|KeyUsage|String|The purpose of the CMK. Default value: ENCRYPT/DECRYPT.|
|DeleteDate|Timestamp|The scheduled date to delete CMK. The time is displayed in UTC. -   If the value is empty, the CMK will not be deleted.
-   This value is returned only when the KeyState value is PendingDeletion.

 |
|Creator|String|The creator of the CMK.|
|Arn|String|The Alibaba Cloud Resource Name \(ARN\) of the CMK.|
|Origin|String|The source of the key material for the CMK.|
|MaterialExpireTime|String|The time when the key material for the CMK expires. The time is displayed in UTC. If the value is empty, the key material for the CMK does not expire.|
|ProtectionLevel|String|The protection level of the CMK.|

## Examples {#section_28947_04 .section}

Sample requests

``` {#codeblock_y9t_tq4_gn9}
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&Description=<your key description>
&KeyUsage=ENCRYPT/DECRYPT
&Origin=<key origin, default Aliyun_KMS>
&ProtectionLevel=HSM
&<Common request parameters>
```

Sample responses

`JSON` format

``` {#codeblock_na5_8jg_hip}
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
                "MaterialExpireTime":"",
                "ProtectionLevel":"HSM"
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

`XML` format

``` {#codeblock_itt_8qv_qm7}
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
        <ProtectionLevel>HSM</ProtectionLevel>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>
```

