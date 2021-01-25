# UpdateCertificateStatus

Updates the status of a certificate.

In this example, the status of the certificate whose ID is `9a28de48-8d8b-484d-a766-dec4****` is updated to REVOKED.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UpdateCertificateStatus&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UpdateCertificateStatus|The operation that you want to perform. Set the value to UpdateCertificateStatus. |
|CertificateId|String|Yes|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Alibaba Cloud Certificate Manager. |
|Status|String|Yes|DISABLED|The status of the certificate. Valid values:

 -   DISABLE: The certificate is disabled.
-   ACTIVE: The certificate is enabled.
-   REVOKED: The certificate is revoked.

**Note:** If the certificate is in the REOVKED state, you can use the certificate only to verify a signature, but not to generate a signature. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|e3f57fe0-9ded-40b0-9caf-a3815f2148c1|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=UpdateCertificateStatus
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&Status=DISABLED
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <RequestId>e3f57fe0-9ded-40b0-9caf-a3815f2148c1</RequestId>
 </KMS>
```

`JSON` format

```
{
	"RequestId": "e3f57fe0-9ded-40b0-9caf-a3815f2148c1"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|Certificate.NotFound|The specified certificate is not found.|The error message returned because the specified certificate does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

