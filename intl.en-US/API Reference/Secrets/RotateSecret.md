# RotateSecret

Manually rotates a secret.

Limits:

• A secret of each Alibaba Cloud account can be rotated for a maximum of 50 times per hour.

• The RotateSecret operation is unavailable for standard secrets.

In this example, the `RdsSecret/Mysql5.4/MyCred` secret is manually rotated, and the version number of the secret is set to `000000123` after the secret is rotated.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=RotateSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|RotateSecret|The operation that you want to perform. Set the value to RotateSecret. |
|SecretName|String|Yes|RdsSecret/Mysql5.4/MyCred|The name of the secret. |
|VersionId|String|Yes|000000123|The version number of the secret after the secret is rotated.

 **Note:** The version number is used to ensure the idempotence of the request. Secrets Manager uses this version number to prevent your application from creating the same version of the secret when the application retries a request. If a version number already exists, Secrets Manager ignores the request for rotation and returns a success message. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:secret/RdsSecret/Mysql5.4/MyCred|The Alibaba Cloud Resource Name \(ARN\) of the secret. |
|SecretName|String|RdsSecret/Mysql5.4/MyCred|The name of the secret. |
|VersionId|String|000000123|The version number of the secret after the secret is rotated. |
|RequestId|String|10257c86-269d-43aa-aaf3-90ed4144bb7c|The ID of the request. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=RotateSecret
&SecretName=RdsSecret/Mysql5.4/MyCred
&VersionId=000000123
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:secret/RdsSecret/Mysql5.4/MyCred</Arn>
	  <SecretName>RdsSecret/Mysql5.4/MyCred</SecretName>
	  <VersionId>000000123</VersionId>
	  <RequestId>10257c86-269d-43aa-aaf3-90ed4144bb7c</RequestId>
</KMS>
```

`JSON` format

```
{
	"Arn": "acs:kms:cn-hangzhou:154035569884****:secret/RdsSecret/Mysql5.4/MyCred",
	"SecretName": "RdsSecret/Mysql5.4/MyCred",
	"VersionId": "000000123",
	"RequestId": "10257c86-269d-43aa-aaf3-90ed4144bb7c"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

