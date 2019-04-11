# DescribeKey {#concept_28952_zh .concept}

Returns detailed information about the specified CMK.

## Request parameters {#section_28952_01 .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK. You can use aliases. For more information, see [Alias Instructions](../../../../../reseller.en-US/User Guide/Alias Instructions.md#).|

## Response parameters {#section_28952_02 .section}

|Name|Type|Description|
|KeyMetadata|[KeyMetadata](#)|Contains metadata about a CMK.|

## KeyMetadata {#section_28952_03 .section}

|Name|Type|Description|
|CreationDate|Timestamp|The date and time \(UTC format\) when the CMK is created.|
|Description|String|The description of the CMK.|
|KeyId|String|The globally unique identifier for the CMK.|
|KeyState|String|The state of the CMK. For more information, see [Impact of CMK states on API call](reseller.en-US/API Reference/Impact of CMK states on API call.md#).|
|KeyUsage|String|Usage of the CMK.|
|DeleteDate|Timestamp|The date and time after which KMS deletes the CMK. For more information, see [ScheduleKeyDeletion](reseller.en-US/API Reference/API list/ScheduleKeyDeletion.md#). This value is present only when `KeyState` is `PendingDeletion`.|
|Creator|String|The creator of the CMK.|
|Arn|String|The Alibaba Cloud Resource Name \(ARN\) of the CMK.|
|Origin|String|The source of the CMK’s key material.|
|MaterialExpireTime|String|The date and time the key expires \(UTC format\). If the value is null, the key does not expire.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeKey
&KeyId=<your-key-id>
&<Common Request Parameters>

```

**Response example**

 `JSON` format

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

 `XML` format

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

