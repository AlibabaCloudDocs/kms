# DescribeAccountKmsStatus

Queries the status of Key Management Service \(KMS\) under your Alibaba Cloud account.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DescribeAccountKmsStatus&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeAccountKmsStatus|The operation that you want to perform. Set the value to DescribeAccountKmsStatus. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|AccountStatus|String|Enabled|The status of KMS under your Alibaba cloud account. Valid values:

 -   Enabled: KMS is enabled.
-   NotEnabled: KMS is disabled.
-   Index: Your account is overdue, and KMS stops providing services.

**Note:** If your Alibaba Cloud account is overdue, top up your account in a timely manner to avoid impacts on your services.

-   Suspended: KMS is suspended. |
|RequestId|String|3455b9b4-95c1-419d-b310-db6a53b09a39|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeAccountKmsStatus
```

Sample success responses

`XML` format

```
<KMS>
    <AccountStatus>Enabled</AccountStatus>
    <RequestId>3455b9b4-95c1-419d-b310-db6a53b09a39</RequestId>
</KMS>
```

`JSON` format

```
{
  "AccountStatus": "Enabled",
  "RequestId": "3455b9b4-95c1-419d-b310-db6a53b09a39"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

