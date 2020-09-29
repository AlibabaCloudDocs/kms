# DeleteSecret

Deletes a secret.

If you call this operation without specifying a recovery period, the deleted secret can be recovered within 30 days.

If you specify a recovery period, the deleted secret can be recovered within the recovery period. You can also forcibly delete a secret. A forcibly deleted secret cannot be recovered.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DeleteSecret&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteSecret|The operation that you want to perform.

 Set the value to **DeleteSecret**. |
|SecretName|String|Yes|secret001|The name of the secret you want to delete. |
|ForceDeleteWithoutRecovery|String|No|false|Specifies whether to forcibly delete the secret. If this parameter is set to true, the secret cannot be recovered.

 Valid values:

 -   **true**
-   **false** \(default value\) |
|RecoveryWindowInDays|String|No|10|Specifies the recovery period of the secret if you do not forcibly delete it. Default value: 30 |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|PlannedDeleteTime|String|2020-02-21T23:36:07.713703651+08:00|The time when the secret is scheduled to be deleted. |
|RequestId|String|38bbed2a-15e0-45ad-98d4-816ad2ccf4ea|The ID of the request. |
|SecretName|String|secret001|The name of the secret. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=DeleteSecret
&SecretName=secret001
&<Common request parameters>
```

Sample success responses

`XML` format

```
<SecretName>secret001</SecretName>
<RequestId>38bbed2a-15e0-45ad-98d4-816ad2ccf4ea</RequestId>
<PlannedDeleteTime>2020-02-21T23:36:07.713703651+08:00</PlannedDeleteTime>
```

`JSON` format

```
{
    "SecretName": "secret001",
    "RequestId": "38bbed2a-15e0-45ad-98d4-816ad2ccf4ea",
    "PlannedDeleteTime": "2020-02-21T23:36:07.713703651+08:00"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

