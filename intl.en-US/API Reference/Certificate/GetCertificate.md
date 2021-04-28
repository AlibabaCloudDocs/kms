# GetCertificate

Queries a certificate that is managed by Certificates Manager.

In this example, the certificate whose ID is `9a28de48-8d8b-484d-a766-dec4****` is queried. The certificate, certificate chain, certificate ID, and certificate signing request \(CSR\) are returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GetCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetCertificate|The operation that you want to perform. Set the value to GetCertificate. |
|CertificateId|String|Yes|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Certificates Manager. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Certificate|String|-----BEGIN CERTIFICATE----- \(X.509 Certificate PEM Content\) -----END CERTIFICATE-----|The certificate in the Privacy Enhanced Mail \(PEM\) format. |
|CertificateChain|String|-----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Sub CA Certificate PEM Content\) -----END CERTIFICATE----- -----BEGIN CERTIFICATE----- \(Root CA Certificate PEM Content\) -----END CERTIFICATE-----|The certificate chain in the PEM format. |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. |
|Csr|String|-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY\*\*\*\*-----END CERTIFICATE REQUEST-----|The CSR in the PEM format. |
|RequestId|String|b3e104b4-0319-4a20-ab7f-9fef6\*\*\*\*|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=GetCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <Csr>-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----</Csr>
	  <RequestId>b3e104b4-0319-4a20-ab7f-9fef6****</RequestId>
	  <CertificateId>9a28de48-8d8b-484d-a766-dec4****</CertificateId>
	  <CertificateChain>-----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Root CA Certificate PEM Content)  -----END CERTIFICATE-----</CertificateChain>
	  <Certificate>-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----</Certificate>
</KMS>
```

`JSON` format

```
{
	"Csr": "-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----",
	"RequestId": "b3e104b4-0319-4a20-ab7f-9fef6****",
	"CertificateId": "9a28de48-8d8b-484d-a766-dec4****",
	"CertificateChain": "-----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Sub CA Certificate PEM Content)  -----END CERTIFICATE-----  -----BEGIN CERTIFICATE-----  (Root CA Certificate PEM Content)  -----END CERTIFICATE-----",
	"Certificate": "-----BEGIN CERTIFICATE-----  (X.509 Certificate PEM Content)  -----END CERTIFICATE-----"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|The error message returned because the specified AccessKey ID does not exist. Check whether a valid AccessKey ID is specified when you call the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

