# OpenKmsService

Activates Key Management Service \(KMS\) under your Alibaba cloud account.

When you call this operation, note that:

-   KMS is a paid service. For more information about the billing method, see [Billing description](~~52608~~).
-   An Alibaba Cloud account can activate KMS only once.
-   Make sure that your Alibaba Cloud account has passed real-name authentication.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=OpenKmsService&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|OpenKmsService|The operation that you want to perform. Set the value to OpenKmsService. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=OpenKmsService
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
      <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` format

```
{
  "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|400|CreateLXOrderFailed|Create order failed.|The error message returned because the order has failed to be created.|
|400|Forbidden.NoRealNameAuthentication|Real name authentication is needed.|The error message returned because you have not completed real-name verification.|
|400|Forbidden.Opened|Your kms service has been opened.|The error message returned because you have activated KMS.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

