# CreateSecret

Creates a secret and stores its initial version.

You must specify the secret name, the secret value stored in the initial version, and the version number. The initial version is marked with ACSCurrent.

You can specify a symmetric customer master key \(CMK\) as the encryption key that is used to protect the secret. If you do not specify a CMK, Secrets Manager creates a CMK to encrypt the secrets that are created by using your Alibaba Cloud account in the current region. Secrets Manager encrypts only the secret value of each version. Secrets Manager does not encrypt the metadata, such as the secret name, version number, and state label.

To use a specified CMK to encrypt a secret value, you must be granted the `kms:GenerateDataKey` permission on the CMK.

In this example, the name of the created secret is `mydbconninfo`, the initial version number is `v1`, and the secret value is `{"user":"root","passwd":"****"}`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateSecret|The operation that you want to perform. Set the value to CreateSecret. |
|SecretData|String|Yes|\{"user":"root","passwd":"\*\*\*\*"\}|The value of the secret that you want to create. Secrets Manager encrypts the secret value and stores the encrypted value in the initial version.

-   If you create a standard secret, you can specify the secret value as required.
-   If you create a managed ApsaraDB RDS secret, the secret value must be in the `{"Accounts":[{"AccountName":"","AccountPassword":""}]}` format. In the preceding format, `AccountName` indicates the username of the account that is used to connect to your ApsaraDB RDS instance, and `AccountPassword` indicates the password of the account. |
|SecretName|String|Yes|mydbconninfo|The name of the secret. |
|VersionId|String|Yes|v1|The initial version number. Version numbers are unique in each secret object. |
|EncryptionKeyId|String|No|00aa68af-2c02-4f68-95fe-3435d330\*\*\*\*|The ID of the Key Management Service \(KMS\) CMK that is used to encrypt the secret value.

If you do not specify this parameter, Secrets Manager automatically creates a CMK to encrypt the secret.

**Note:** The KMS CMK must be a symmetric key. |
|SecretDataType|String|No|text|The type of the secret value. Valid values:

-   text
-   binary

**Note:** Set the SecretDataType parameter to text if you create a managed ApsaraDB RDS secret. |
|Description|String|No|mydbinfo|The description of the secret. |
|Tags|String|No|\[\{\\"TagKey\\":\\"key1\\",\\"TagValue\\":\\"val1\\"\},\{\\"TagKey\\":\\"key2\\",\\"TagValue\\":\\"val2\\"\}\]|The tag of the secret. |
|SecretType|String|No|Rds|The type of the secret. Valid values:

-   Generic: indicates a standard secret.
-   Rds: indicates a managed ApsaraDB RDS secret. |
|ExtendedConfig|Json|No|\{"SecretSubType":"SingleUser", "DBInstanceId":"rm-bp1b3dd3a506e\*\*\*\*" ,"CustomData":\{\}\}|The extended configuration of the secret. This parameter specifies the properties for a specific secret type. The value can be up to 1,024 characters in length and is in the JSON map format.

-   If the SecretType parameter is set to Generic, you do not need to specify this parameter.
-   If the SecretType parameter is set to Rds, you must specify the following fields in the ExtendedConfig parameter:
    -   SecretSubType: the subtype of the secret. This field is required. Valid values:
        -   SingleUser: indicates that Secrets Manager manages the ApsaraDB RDS secret in single account mode. When the secret is rotated, the password for the specified account is reset to a new random password.
        -   DoubleUsers: indicates that Secrets Manager manages the ApsaraDB RDS secret in double-account mode. One account is referenced by the ACSCurrent version, and the other account is referenced by the ACSPrevious version. When the secret is rotated, the password for the account referenced by the ACSPrevious version is reset to a new random password. Then, Secrets Manager switches the referenced accounts between the ACSCurrent and ACSPrevious versions.
    -   DBInstanceId: the ApsaraDB RDS instance to which the ApsaraDB RDS account belongs. This field is required.
    -   CustomData: the custom data. This field is optional. The value is a collection of key-value pairs in the JSON format. A maximum of 10 key-value pairs can be specified. Separate multiple key-value pairs with commas \(,\). Example: `{"Key1": "v1", "fds":"fdsf"}`. Default value: `{}`. |
|EnableAutomaticRotation|Boolean|No|true|Specifies whether to enable automatic rotation. Valid values:

-   true: indicates that automatic rotation is enabled.
-   false: indicates that automatic rotation is disabled. This is the default value.

**Note:** This parameter takes effect only when the SecretType parameter is set to Rds. |
|RotationInterval|String|No|30d|The interval for automatic rotation. Valid values: 6 hours to 8,760 hours \(365 days\).

Specify the interval in the `integer[unit]` format, where `integer` indicates the interval and `unit` indicates the time unit.

The unit can be d \(day\), h \(hour\), m \(minute\), or s \(second\). For example, both 7d and 604800s indicate a seven-day interval.

**Note:** If the EnableAutomaticRotation parameter is set to true, this parameter is required. Otherwise, you do not need to specify this parameter. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/mydbconninfo|The Alibaba Cloud Resource Name \(ARN\). |
|AutomaticRotation|String|Enabled|Indicates whether automatic rotation is enabled. Valid values:

-   Enabled: indicates that automatic rotation is enabled.
-   Disabled: indicates that automatic rotation is disabled.
-   Invalid: indicates that the status of automatic rotation is abnormal. Secrets Manager cannot automatically rotates the secret.

**Note:** This parameter is returned if the value of the SecretType parameter is Rds. |
|ExtendedConfig|String|\{\\"SecretSubType\\":\\"SingleUser\\", \\"DBInstanceId\\":\\"rm-uf667446pc955\*\*\*\*\\", \\"CustomData\\":\{\} \}|The extended configuration of the secret. This parameter is returned if the value of the SecretType parameter is Rds. |
|NextRotationDate|String|2020-07-06T18:22:03Z|The time when the next rotation is scheduled for execution.

**Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|RequestId|String|3bf02f7a-015b-4f93-be0f-cc043fda2dd3|The ID of the request. |
|RotationInterval|String|604800s|The interval for automatic rotation.

The interval is in the `integer[unit]` format, where `integer` indicates the interval, and `unit` indicates the time unit. The `unit` field has a fixed value of s. For example, 604800s indicates a seven-day interval.

**Note:** This parameter is returned if the value of the AutomaticRotation parameter is Enabled or Invalid. |
|SecretName|String|mydbconninfo|The name of the secret. |
|SecretType|String|Rds|The type of the secret. |
|VersionId|String|v1|The version number of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=CreateSecret
&SecretData={"user":"root","passwd":"****"}
&SecretName=mydbconninfo
&VersionId=v1
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
      <Arn>acs:kms:cn-hangzhou:154035569884****:secret/mydbconninfo</Arn>
      <SecretName>mydbconninfo</SecretName>
      <VersionId>v1</VersionId>
      <RequestId>3bf02f7a-015b-4f93-be0f-cc043fda2dd3</RequestId>
      <SecretType>Generic</SecretType>
 </KMS>
```

`JSON` format

```
{
    "Arn": "acs:kms:cn-hangzhou:154035569884****:secret/mydbconninfo",
    "SecretName": "mydbconninfo",
    "VersionId": "v1",
    "RequestId": "3bf02f7a-015b-4f93-be0f-cc043fda2dd3",
    "SecretType": "Generic"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|InvalidParameter|The specified parameter is invalid.|The error message returned because one or more parameters are invalid.|
|400|Rejected.LimitExceeded|The secret quota is exceeded.|The error message returned because the secret quota is full.|
|403|Forbidden.NoPermission|You are not authorized to perform the operation.|The error message returned because you are not authorized to perform the operation.|
|404|Forbidden.ResourceNotFound|The resource is not found.|The error message returned because the specified resource does not exist.|
|409|Rejected.ResourceExist|The resource already exists.|The error message returned because the specified resource already exists.|
|409|Rejected.ResourceInDeleteWindow|The secret is planned to be deleted.|The error message returned because the secret is to be deleted.|
|500|InternalFailure|An internal error occurred.|The error message returned because an internal error occurred.|
|429|Rejected.Throttling|The QPS upper limit is exceeded.|The error message returned because the queries per second \(QPS\) has reached the upper limit.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

