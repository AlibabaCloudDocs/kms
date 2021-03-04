# DescribeSecret

Obtains the metadata of a secret.

This operation returns the metadata information stored in a secret object and does not return the encrypted secret value.

In this example, the metadata information of the `secret001` secret is returned. The metadata information includes the Alibaba Cloud Resource Name \(ARN\) of the secret, secret name, secret type, secret description, the time when the secret was created and updated, information about automatic rotation, and extended configuration of the secret.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DescribeSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeSecret|The operation that you want to perform. Set the value to DescribeSecret. |
|SecretName|String|Yes|secret001|The name of the secret. |
|FetchTags|String|No|true|Specifies whether to return the resource tags of the secret. Valid values:

 -   true: The resource tags are returned.
-   false: The resource tags are not returned. This is the default value. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/secret001|The ARN of the secret. |
|AutomaticRotation|String|Enabled|Indicates whether automatic rotation is enabled. Valid values:

 -   Enabled: indicates that automatic rotation is enabled.
-   Disabled: indicates that automatic rotation is disabled.
-   Invalid: indicates that the status of automatic rotation is abnormal. Secrets Manager cannot automatically rotate the secret.

 **Note:** This parameter is returned only for managed ApsaraDB RDS secrets. |
|CreateTime|String|2020-02-21T15:39:26Z|The time when the secret was created. |
|Description|String|userinfo|The description of the secret. |
|EncryptionKeyId|String|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|The ID of the Key Management Service \(KMS\) customer master key \(CMK\) that is used to encrypt the secret value. |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|The extended configuration of the secret.

 **Note:** This parameter is returned only for managed ApsaraDB RDS secrets. |
|LastRotationDate|String|2020-07-05T08:22:03Z|The time when the last rotation was performed.

 **Note:** This parameter is returned if the secret was rotated. |
|NextRotationDate|String|2020-07-06T18:22:03Z|The time when the next rotation is scheduled for execution.

 **Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|PlannedDeleteTime|String|2020-03-21T15:45:12Z|The time when the secret is scheduled to be deleted. |
|RequestId|String|93348dfb-3627-4417-8d90-487a76a909c9|The ID of the request. |
|RotationInterval|String|3153600s|The interval for automatic rotation.

 The interval is in the `integer[unit]` format, where `integer` indicates the interval, and `unit` indicates the time unit. The `unit` field has a fixed value of s. For example, 604800s indicates a seven-day interval.

 **Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|SecretName|String|secret001|The name of the secret. |
|SecretType|String|Rds|The type of the secret. Valid values:

 -   Generic: indicates a standard secret.
-   Rds: indicates a managed ApsaraDB RDS secret. |
|Tags|Array of Tag| |The resource tags of the secret.

 If the FetchTags parameter is set to false or is not specified, this parameter is not returned. |
|Tag| | | |
|TagKey|String|key1|The tag key. |
|TagValue|String|val1|The tag value. |
|UpdateTime|String|2020-02-21T15:39:26Z|The time when the secret was updated. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeSecret
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:secret/secret001</Arn>
	  <SecretName>secret001</SecretName>
	  <Description>userinfo</Description>
	  <CreateTime>2021-01-08T10:50:05Z</CreateTime>
	  <UpdateTime>2021-01-08T10:50:05Z</UpdateTime>
	  <RequestId>93f84812-66d2-467a-9aec-61f6f53919dc</RequestId>
	  <SecretType>Rds</SecretType>
	  <AutomaticRotation>Disabled</AutomaticRotation>
	  <ExtendedConfig>{"SecretSubType":"SingleUser", "DBInstanceId":"rm-uf667446pc955****",  "CustomData":{} }</ExtendedConfig>
</KMS>
```

`JSON` format

```
{
	"Arn": "acs:kms:cn-hangzhou:154035569884****:secret/secret001",
	"SecretName": "secret001",
	"Description": "userinfo",
	"CreateTime": "2021-01-08T10:50:05Z",
	"UpdateTime": "2021-01-08T10:50:05Z",
	"RequestId": "93f84812-66d2-467a-9aec-61f6f53919dc",
	"SecretType": "Rds",
	"AutomaticRotation": "Disabled",
	"ExtendedConfig": "{\"SecretSubType\":\"SingleUser\", \"DBInstanceId\":\"rm-uf667446pc955****\",  \"CustomData\":{} }"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

