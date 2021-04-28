# UploadCertificate

Imports a certificate and certificate chain issued by a certificate authority \(CA\) into Certificates Manager.

In this example, a certificate issued by a CA is imported into Certificates Manager. The ID of the certificate in Certificates Manager is `12345678-1234-1234-1234-12345678****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=UploadCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|UploadCertificate|The operation that you want to perform. Set the value to UploadCertificate. |
|Certificate|String|Yes|-----BEGIN CERTIFICATE----- \(X.509 Certificate PEM Content\) -----END CERTIFICATE-----|The certificate issued by the CA, which is in the Privacy Enhanced Mail \(PEM\) format. |
|CertificateId|String|Yes|12345678-1234-1234-1234-12345678\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Certificates Manager. |
|CertificateChain|String|No|-----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Root CA Certificate PEM Content\) -----END CERTIFICATE-----|The certificate chain issued by the CA, which is in the PEM format. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|RequestId|String|15a735a1-8fe6-45cc-a64c-3c4ff839334e|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=UploadCertificate
&Certificate=-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----
&CertificateId=12345678-1234-1234-1234-12345678****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
        <RequestId>15a735a1-8fe6-45cc-a64c-3c4ff839334e</RequestId>
</KMS>
```

`JSON` format

```
{
    "RequestId": "15a735a1-8fe6-45cc-a64c-3c4ff839334e"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|The error message returned because the specified AccessKey ID does not exist. Check whether a valid AccessKey ID is specified when you call the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

