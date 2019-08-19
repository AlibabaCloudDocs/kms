# DescribeKey {#concept_28952_zh .concept}

You can call this operation to query detailed information about a specified CMK.

## Request parameters {#section_28952_01 .section}

|Parameter|Type|Required|Description|
|KeyId|String|Yes|The globally unique ID of the CMK to query. You can use aliases in the request. For more information, see [Alias Instructions](../../../../reseller.en-US/User Guide/Alias Instructions.md#).|

## Response parameters {#section_28952_02 .section}

|Parameter|Type|Description|
|KeyMetadata|[KeyMetadata parameters](#section_28952_03)|The metadata of the CMK queried.|

## KeyMetadata parameters {#section_28952_03 .section}

|Parameter|Type|Description|
|CreationDate|Timestamp|The date and time when the CMK was created. The time is displayed in UTC.|
|Description|String|The description of the CMK.|
|KeyId|String|The globally unique ID of the CMK.|
|KeyState|String|The status of the CMK. For more information, see [Impact of CMK states on API call](reseller.en-US/API Reference/Impact of CMK states on API call.md#).|
|KeyUsage|String|The purpose of the CMK.|
|DeleteDate|Timestamp|The scheduled period before the CMK is deleted. For more information, see [ScheduleKeyDeletion](reseller.en-US/API Reference/API list/ScheduleKeyDeletion.md#). This value is returned only when the KeyState value is PendingDeletion.|
|Creator|String|The creator of the CMK.|
|Arn|String|The Alibaba Cloud Resource Name \(ARN\) of the CMK.|
|Origin|String|The source of the key material for the CMK.|
|MaterialExpireTime|String|The time when the key material for the CMK expires. The time is displayed in UTC. If the value is empty, the key material for the CMK does not expire.|
|ProtectionLevel|String|The protection level of the CMK.|

## Examples {#section_qpb_yao_9gf .section}

Sample requests

``` {#codeblock_cua_lpn_ph6}
https://kms.cn-hangzhou.aliyuncs.com/?Action=DescribeKey
&KeyId=<your-key-id>
&<Common request parameters>
```

Sample responses

`JSON` format

``` {#codeblock_evq_bp7_mrg}
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
                "MaterialExpireTime":"",
                "ProtectionLevel":"HSM"
        },
        "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

`XML` format

``` {#codeblock_zim_dmw_wid}
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
        <ProtectionLevel>HSM</ProtectionLevel>
 </KeyMetadata>
 <RequestId>6cb4bf6b-d9c9-4660-af5f-2328378e7257</RequestId>
</KMS>
```

