# PutSecretValue

Stores the secret value of a new version into a secret object.

This operation is used to store secret values of new versions. It cannot be used to modify the secret value of an existing version.

By default, the newly stored secret value is marked with ACSCurrent, and the original version marked with ACSCurrent is marked with ACSPrevious. If you specify the VersionStage parameter, the newly stored secret value is marked with the specified stage label.

You must specify a version number. Secrets Manager performs operations based on the following rules:

-   If the specified version number does not exist in the secret object, Secrets Manager creates the new version and stores the secret value.
-   If the specified version number already exists in the secret object and the secret value of the existing version is the same as the secret value that you specify, Secrets Manager ignores the request and returns a success message. The request is idempotent.
-   If the specified version number already exists in the secret object but the secret value of the existing version is different from the secret value that you specify, Secrets Manager rejects the request and returns a failure message.

Limits: This operation is available only for standard secrets.

In this example, the secret value of a new version is stored into the `secret001` secret. The `VersionId` parameter is set to `00000000000000000000000000000000203`, and the `SecretData` parameter is set to `importantdata`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=PutSecretValue&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|PutSecretValue|The operation that you want to perform. Set the value to PutSecretValue. |
|SecretData|String|Yes|importantdata|The secret value. It is encrypted and then stored in a specified new version. |
|SecretName|String|Yes|secret001|The name of the secret. |
|VersionId|String|Yes|00000000000000000000000000000000203|The version number of the secret value that you want to store. Version numbers are unique in each secret object. |
|SecretDataType|String|No|text|The type of the secret value. Valid values:

 -   text: This is the default value.
-   binary |
|VersionStages|String|No|\{"VersionStage": \[ "ACSCurrent" \] \}|The stage label that marks the new secret version. If you do not specify this parameter, Secrets Manager marks it with ACSCurrent. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |
|VersionId|String|00000000000000000000000000000000203|The version number of the secret value. |
|VersionStages|List|\{"VersionStage": \["ACSCurrent"\]\}|The stage labels that mark the version. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=PutSecretValue
&SecretData=importantdata
&SecretName=secret001
&VersionId=00000000000000000000000000000000203
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretName>secret001</SecretName>
	  <VersionId>00000000000000000000000000000000203</VersionId>
	  <VersionStages>
		    <VersionStage>ACSCurrent</VersionStage>
	  </VersionStages>
	  <RequestId>f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8</RequestId>
</KMS>
```

`JSON` format

```
{
	"SecretName": "secret001",
	"VersionId": "00000000000000000000000000000000203",
	"VersionStages": {
		"VersionStage": [
			"ACSCurrent"
		]
	},
	"RequestId": "f94ec9d3-2d10-4922-9a5c-5dcd5ebcb5e8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

