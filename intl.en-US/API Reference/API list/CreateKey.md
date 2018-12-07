# CreateKey {#concept_28947_zh .concept}

Creates a customer master key \(CMK\).

You can use a CMK to encrypt small amounts of data \(a maximum of 6 KB\). Typically, you use CMKs to generate data keys that you can use to encrypt large amounts of data. For more information, see [GenerateDataKey](reseller.en-US/API Reference/API list/GenerateDataKey.md#).

## Request parameters {#section_28947_01 .section}

|Name|Type|Required|Description|
|Origin|String|No|The source of the key material for the CMK.Valid values: Aliyun\_KMS and EXTERNAL.

**Note:** Default value: Aliyun\_KMS. Note that the values are case sensitive.

If you choose EXTERNAL, you need to [Import key material](../../../../reseller.en-US/User Guide/Import key material.md#).|
|Description|String|No|The description of the CMK. Length constraints: Minimum length of 0 characters. Maximum length of 8192 characters.|
|KeyUsage|String|No|The intended use of the CMK. Default value: ENCRYPT/DECRYPT.|

## Response parameters {#section_28947_02 .section}

|Name|Type|Description|
|KeyMetadata|[KeyMetadata](#section_28947_03)|The metadata associated with the CMK.|

## KeyMetadata {#section_28947_03 .section}

|Name|Type|Description|
|CreationDate|Timestamp|The date and time \(in UTC format\) when the CMK is created.|
|Description|String|The description of the CMK.|
|KeyId|String|The globally unique identifier for the CMK.|
|KeyState|String|The state of the CMK. For more information, see [Impact of CMK states on API call](reseller.en-US/API Reference/Impact of CMK states on API call.md#).|
|KeyUsage|String|The cryptographic operations for which you can use the CMK. Valid Values: ENCRYPT/DECRYPT.|
|DeleteDate|Timestamp|The date and time after which KMS deletes the CMK.-   A null value indicates that the CMK is not to be deleted.
-   This value is present only when `KeyState` is **PendingDeletion**.

|
|Creator|String|The creator of the CMK.|
|Arn|String|The Alibaba Cloud Resource Name \(ARN\) of the CMK.|
|Origin|String|The source of the CMK’s key material.|
|MaterialExpireTime|String|The time at which the imported key material expires. If the value is null, the key does not expire.|

## Examples {#section_28947_04 .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=CreateKey
&Description=<your key description>
&KeyUsage=ENCRYPT/DECRYPT
&Origin=<key origin, default Aliyun_KMS>
&<Common request parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "KeyMetadata": {
                "CreationDate": "2016-03-25T10:42:40Z",
                "Description": "key description example",
                "KeyId": "08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4fb73",
                "KeyState": "Enabled",
                "KeyUsage": "ENCRYPT/DECRYPT",
                "DeleteDate": "",
                "Creator":"123456",
                "Arn":"acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4fb73",
                "Origin":"Aliyun_KMS",
                "MaterialExpireTime":""
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}


```

 `XML` format

```
//xml response
<KMS>
 <KeyMetadata>
        <CreationDate>2016-03-25T10:40:47Z</CreationDate>
        <Description>key description example</Description>
        <KeyId>08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4fb73</KeyId>
        <KeyState>Enabled</KeyState>
        <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
        <DeleteDate></DeleteDate>
        <Creator>123456</Creator>
        <Arn>acs:kms:cn-hangzhou:123456:key/08c33a6f-4e0a-4a1b-a3fa-7ddfa1d4fb73</Arn>
        <Origin>Aliyun_KMS</Origin>
        <MaterialExpireTime></MaterialExpireTime>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>


```

