# UpdateSecretRotationPolicy

Updates the rotation policy of a secret.

After automatic rotation is enabled, Secrets Manager schedules the first automatic rotation by adding the preset rotation interval to the timestamp of the last rotation.

Limits: The UpdateSecretRotationPolicy operation cannot be used to update the rotation policy of standard secrets.

In this example, the rotation policy of the `RdsSecret/Mysql5.4/MyCred` secret is updated in the following way:

-   The `EnableAutomaticRotation` parameter is set to `true`, which indicates that automatic rotation is enabled.
-   The `RotationInterval` parameter is set to `30d`, which indicates that the interval for automatic rotation is 30 days.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateSecretRotationPolicy&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateSecretRotationPolicy|The operation that you want to perform. Set the value to UpdateSecretRotationPolicy. |
|EnableAutomaticRotation|Boolean|Yes|true|Specifies whether to enable automatic rotation. Valid values:

 -   true: indicates that automatic rotation is enabled.
-   false: indicates that automatic rotation is disabled. This is the default value. |
|SecretName|String|Yes|RdsSecret/Mysql5.4/MyCred|The name of the secret. |
|RotationInterval|String|No|30d|The interval for automatic rotation. Valid values: 6 hours to 8,760 hours \(365 days\).

 Specify the interval in the `integer[unit]` format, where `integer` indicates the interval and `unit` indicates the time unit.

 The unit can be d \(day\), h \(hour\), m \(minute\), or s \(second\). For example, both 7d and 604800s indicate a seven-day interval.

 **Note:** If the EnableAutomaticRotation parameter is set to true, this parameter is required. Otherwise, you do not need to specify this parameter. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|SecretName|String|RdsSecret/Mysql5.4/MyCred|The name of the secret. |
|RequestId|String|2c124f6f-4210-499f-b88a-69f54004d2d8|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=UpdateSecretRotationPolicy
&EnableAutomaticRotation=true
&SecretName=RdsSecret/Mysql5.4/MyCred
&RotationInterval=30d
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <SecretName>RdsSecret/Mysql5.4/MyCred</SecretName>
	  <RequestId>2c124f6f-4210-499f-b88a-69f54004d2d8</RequestId>
</KMS>
```

`JSON` format

```
{
    "SecretName": "RdsSecret/Mysql5.4/MyCred",
    "RequestId": "2c124f6f-4210-499f-b88a-69f54004d2d8"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

