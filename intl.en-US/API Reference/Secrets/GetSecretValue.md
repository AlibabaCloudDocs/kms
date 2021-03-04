# GetSecretValue

Obtains a secret value.

If you do not specify a version number or stage label, Secrets Manager returns the secret value of the version marked with ACSCurrent.

If a Key Management Service \(KMS\) customer master key \(CMK\) is specified to encrypt the secret value, you must have the `kms:Decrypt` permission on the CMK to call this operation.

In this example, the value of the `secret001` secret is returned in the `SecretData` parameter, which is `testdata1`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GetSecretValue&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetSecretValue|The operation that you want to perform. Set the value to GetSecretValue. |
|SecretName|String|Yes|secret001|The name of the secret. |
|VersionStage|String|No|ACSCurrent|The stage label that marks the secret version. If you specify this parameter, Secrets Manager returns the secret value of the version that is marked with the specified stage label.

 Default value: ACSCurrent.

 **Note:** For managed ApsaraDB RDS secrets, Secrets Manager returns only the secret values of the versions marked with ACSPrevious and ACSCurrent. |
|VersionId|String|No|00000000000000000000000000000001|The version number of the secret value. If you specify this parameter, Secrets Manager returns the secret value of the specified version.

 **Note:** The VersionId parameter is unavailable for managed ApsaraDB RDS secrets. If you specify this parameter for a managed ApsaraDB RDS secret, this parameter does not take effect. |
|FetchExtendedConfig|Boolean|No|true|Specifies whether to obtain the extended configuration of the secret. Valid values:

 -   true
-   false: This is the default value.

 **Note:** This parameter does not take effect for standard secrets. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AutomaticRotation|String|Enabled|Indicates whether automatic rotation is enabled. Valid values:

 -   Enabled: indicates that automatic rotation is enabled.
-   Disabled: indicates that automatic rotation is disabled.
-   Invalid: indicates that the status of automatic rotation is abnormal. Secrets Manager cannot automatically rotate the secret.

 **Note:** This parameter is returned only for managed ApsaraDB RDS secrets. |
|CreateTime|String|2020-02-21T15:39:26Z|The time when the secret was created. |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|The extended configuration of the secret. This parameter is returned if the value of the SecretType parameter is Rds and the FetchExtendedConfig parameter is set to true. |
|LastRotationDate|String|2020-07-05T08:22:03Z|The time when the last rotation was performed.

 **Note:** This parameter is returned if the secret was rotated. |
|NextRotationDate|String|2020-07-06T18:22:03Z|The time when the next rotation is scheduled for execution.

 **Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|RequestId|String|6a3e9c36-1150-4881-84d3-eb8672fcafad|The ID of the request. |
|RotationInterval|String|604800s|The interval for automatic rotation.

 The interval is in the `integer[unit]` format, where `integer` indicates the interval, and `unit` indicates the time unit. The `unit` field has a fixed value of s. For example, 604800s indicates a seven-day interval.

 **Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|SecretData|String|testdata1|The secret value. Secrets Manager decrypts the stored secret value in ciphertext and returns the secret value.

 The secret value returned by managed ApsaraDB RDS secrets is in the following format:

 `{"AccountName":"","AccountPassword":""}`|
|SecretDataType|String|binary|The type of the secret value. Valid values:

 -   text
-   binary |
|SecretName|String|secret001|The name of the secret. |
|SecretType|String|Generic|The type of the secret. Valid values:

 -   Generic: indicates a standard secret.
-   Rds: indicates a managed ApsaraDB RDS secret. |
|VersionId|String|00000000000000000000000000000001|The version number of the secret value. |
|VersionStages|List|\{ "VersionStage": \[ "ACSCurrent" \] \}|The stage labels that mark the secret version. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=GetSecretValue
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <VersionId>00000000000000000000000000000001</VersionId>
	  <SecretData>testdata1</SecretData>
	  <SecretType>Generic</SecretType>
	  <SecretDataType>binary</SecretDataType>
	  <VersionStages>
		    <VersionStage>ACSCurrent</VersionStage>
	  </VersionStages>
	  <CreateTime>2020-07-23T11:56:29Z</CreateTime>
	  <RequestId>6a3e9c36-1150-4881-84d3-eb8672fcafad</RequestId>
</KMS>
```

`JSON` format

```
{
	"SecretName": "secret001",
	"VersionId": "00000000000000000000000000000001",
	"SecretData": "testdata1",
	"SecretType": "Generic",
	"SecretDataType": "binary",
	"VersionStages": {
		"VersionStage": [
			"ACSCurrent"
		]
	},
	"CreateTime": "2020-07-23T11:56:29Z",
	"RequestId": "6a3e9c36-1150-4881-84d3-eb8672fcafad"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

