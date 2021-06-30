# DescribeKey

Queries the information about a customer master key \(CMK\).

You can query the information about the CMK `05754286-3ba2-4fa6-8d41-4323aca6****` by using parameter settings provided in this topic. The information includes the creator, creation time, status, and deletion protection status of the CMK.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DescribeKey&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeKey|The operation that you want to perform. Set the value to DescribeKey. |
|KeyId|String|Yes|05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|The ID of the CMK.

You can also set this parameter to an alias that is bound to the CMK. For more information, see [Overview of aliases](~~68522~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|KeyMetadata|Struct| |The metadata of the CMK. |
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:key/05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the CMK. |
|AutomaticRotation|String|Disabled|Indicates whether automatic rotation is enabled. Valid values:

-   Enabled
-   Disabled
-   Suspended

For more information, see [Automatic key rotation](~~134270~~).

**Note:** Only symmetric CMKs support automatic rotation. |
|CreationDate|String|2021-05-20T06:34:21Z|The time when the CMK was created. The time is displayed in UTC. |
|Creator|String|154035569884\*\*\*\*|The user who created the CMK. The value is an Alibaba Cloud account. |
|DeleteDate|String|2021-05-26T18:22:03Z|The time at which the CMK is scheduled for deletion. The time is displayed in UTC.

For more information, see [ScheduleKeyDeletion](~~44196~~).

**Note:** This parameter is returned only when the value of the KeyState parameter is PendingDeletion. |
|DeletionProtection|String|Enabled|Indicates whether deletion protection is enabled. Valid values:

-   Enabled
-   Disabled |
|DeletionProtectionDescription|String|The CMK is being used by XXX. Deletion protection is set.|The description of deletion protection. |
|Description|String|key description example|The description of the CMK. |
|KeyId|String|05754286-3ba2-4fa6-8d41-4323aca6\*\*\*\*|The ID of the CMK. |
|KeySpec|String|Aliyun\_AES\_256|The type of the CMK. |
|KeyState|String|Enabled|The status of the CMK.

For more information, see [Impact of CMK status on API operations](~~44211~~). |
|KeyUsage|String|ENCRYPT/DECRYPT|The purpose of the CMK. |
|LastRotationDate|String|2021-05-20T06:34:21Z|The time when the last rotation was performed. The time is displayed in UTC. For a new CMK, the value of this parameter is the time when the initial version of the CMK was generated. |
|MaterialExpireTime|String|2021-07-06T18:22:03Z|The time when the key material of the CMK expires. The time is displayed in UTC. If the value is empty, the key material of the CMK does not expire. |
|NextRotationDate|String|2021-07-06T18:22:03Z|The time at which the next rotation is scheduled for execution.

**Note:** This parameter is returned only when the value of the AutomaticRotation parameter is Enabled or Suspended. |
|Origin|String|Aliyun\_KMS|The source of the key material for the CMK. |
|PrimaryKeyVersion|String|515e0b0a-624f-45ab-92b5-54f9b551\*\*\*\*|The ID of the current primary key version for the symmetric CMK. |
|ProtectionLevel|String|HSM|The protection level of the CMK. |
|RotationInterval|String|31536000s|The interval for automatic rotation.

Unit: seconds.

For example, if the value is 604800s, automatic rotation is performed at a 7-day interval.

**Note:** This parameter is returned only when the value of the AutomaticRotation parameter is Enabled or Suspended. |
|RequestId|String|f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DescribeKey
&KeyId=05754286-3ba2-4fa6-8d41-4323aca6****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
      <KeyMetadata>
            <CreationDate>2021-05-20T06:34:21Z</CreationDate>
            <Description></Description>
            <KeyId>05754286-3ba2-4fa6-8d41-4323aca6****</KeyId>
            <KeySpec>Aliyun_AES_256</KeySpec>
            <KeyState>Enabled</KeyState>
            <KeyUsage>ENCRYPT/DECRYPT</KeyUsage>
            <PrimaryKeyVersion>515e0b0a-624f-45ab-92b5-54f9b551****</PrimaryKeyVersion>
            <DeleteDate></DeleteDate>
            <Creator>154035569884****</Creator>
            <Arn>acs:kms:cn-hangzhou:154035569884****:key/05754286-3ba2-4fa6-8d41-4323aca6****</Arn>
            <Origin>Aliyun_KMS</Origin>
            <MaterialExpireTime></MaterialExpireTime>
            <ProtectionLevel>HSM</ProtectionLevel>
            <LastRotationDate>2021-05-20T06:34:21Z</LastRotationDate>
            <AutomaticRotation>Disabled</AutomaticRotation>
            <DeletionProtection>Enabled</DeletionProtection>
      </KeyMetadata>
      <RequestId>f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f</RequestId>
</KMS>
```

`JSON` format

```
{
    "KeyMetadata": {
        "CreationDate": "2021-05-20T06:34:21Z",
        "Description": "",
        "KeyId": "05754286-3ba2-4fa6-8d41-4323aca6****",
        "KeySpec": "Aliyun_AES_256",
        "KeyState": "Enabled",
        "KeyUsage": "ENCRYPT/DECRYPT",
        "PrimaryKeyVersion": "515e0b0a-624f-45ab-92b5-54f9b551****",
        "DeleteDate": "",
        "Creator": "154035569884****",
        "Arn": "acs:kms:cn-hangzhou:154035569884****:key/05754286-3ba2-4fa6-8d41-4323aca6****",
        "Origin": "Aliyun_KMS",
        "MaterialExpireTime": "",
        "ProtectionLevel": "HSM",
        "LastRotationDate": "2021-05-20T06:34:21Z",
        "AutomaticRotation": "Disabled",
        "DeletionProtection": "Enabled"
    },
    "RequestId": "f1fdfa9d-bd49-418b-942f-8f3e3ec00a4f"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|Forbidden.KeyNotFound|The specified Key is not found.|The error message returned because the specified CMK is not found.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

