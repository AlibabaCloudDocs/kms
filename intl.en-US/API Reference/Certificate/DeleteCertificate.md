# DeleteCertificate

Deletes a certificate and its private key and certificate chain.

After the certificate and its private key and certificate chain are deleted, they cannot be restored. Proceed with caution.

In this example, the certificate whose ID is `9a28de48-8d8b-484d-a766-dec4****` and its private key and certificate chain are deleted.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DeleteCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DeleteCertificate|The operation that you want to perform. Set the value to DeleteCertificate. |
|CertificateId|String|Yes|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Alibaba Cloud Certificate Manager. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DeleteCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <RequestId>d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0</RequestId>
</KMS>
```

`JSON` format

```
{
	"RequestId": "d97f6c33-ca26-4de2-a580-0e2fd1c5bfb0"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|Certificate.NotFound|The specified certificate is not found.|The error message returned because the specified certificate does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

