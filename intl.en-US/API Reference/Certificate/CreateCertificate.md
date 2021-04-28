# CreateCertificate

Creates a certificate.

To create a certificate, you must specify an asymmetric key type, generate a private key in Certificates Manager, and then obtain the certificate signing request \(CSR\). Submit the CSR in the Privacy Enhanced Mail \(PEM\) format to a certificate authority \(CA\) to obtain the formal certificate and certificate chain. Then, call the [UploadCertificate](~~212136~~) operation to import the certificate into Certificates Manager.

In this example, a certificate is created and the CSR is obtained.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCertificate|The operation that you want to perform. Set the value to CreateCertificate. |
|KeySpec|String|Yes|RSA\_2048|The type of the key. Valid values:

 -   RSA\_2048
-   EC\_P256
-   EC\_SM2 |
|Subject|String|Yes|CN=userName,OU=kms,O=aliyun,C=CN|The certificate subject, which is the owner of the certificate.

 The value is in the distinguished name \(DN\) format, as defined in [RFC 2253](https://tools.ietf.org/html/rfc2253?spm=a2c4g.11186623.2.13.265f1a1cGFCn3Q). A DN is a sequence of relative distinguished names \(RDNs\).

 RDNs are key-value pairs in the format of `attribute1=value1,attribute2=value2`. Separate multiple RDNs with commas \(,\).

 The Subject parameter consists of the following fields:

 -   CN: required. The name of the certificate subject.
-   C: required. The two-character country or region code in the [ISO 3166-1](https://www.iso.org/obp/ui/#search/code/) standard. For example, CN indicates China.
-   O: required. The legal name of the enterprise, company, organization, or institution.
-   OU: required. The name of the department.
-   ST: optional. The name of the province, municipality, autonomous region, or special administrative region.
-   L: optional. The name of the city. |
|SubjectAlternativeNames|Json|No|\["test1.example.com","test2.example.com"\]|The subject alternative names.

 A domain name list is supported. A maximum of 10 domain names are supported. |
|ExportablePrivateKey|Boolean|No|true|Specifies whether the private key of the certificate can be exported for use. Valid values:

 -   true: The private key of the certificate can be exported for use. This is the default value.
-   false: The private key of the certificate cannot be exported for use. We recommend that you set this parameter to false to protect keys with a higher security level. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:certificate/98e85c94-52d0-40c9-b3b2-afda52f4\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\) of the certificate. |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Certificates Manager. |
|Csr|String|-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY\*\*\*\*-----END CERTIFICATE REQUEST-----|The CSR in the PEM format. |
|RequestId|String|15a735a1-8fe6-45cc-a64c-3c4ff839334e|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CreateCertificate
&KeySpec=RSA_2048
&Subject=CN=userName,OU=kms,O=aliyun,C=CN
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <CertificateId>98e85c94-52d0-40c9-b3b2-afda52f4****</CertificateId>
	  <Arn>acs:kms:cn-hangzhou:154035569884****:certificate/98e85c94-52d0-40c9-b3b2-afda52f4****</Arn>
	  <Csr>-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----</Csr>
	  <RequestId>15a735a1-8fe6-45cc-a64c-3c4ff839334e</RequestId>
</KMS>
```

`JSON` format

```
{
	"CertificateId": "98e85c94-52d0-40c9-b3b2-afda52f4****",
	"Arn": "acs:kms:cn-hangzhou:154035569884****:certificate/98e85c94-52d0-40c9-b3b2-afda52f4****",
	"Csr": "-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY****-----END CERTIFICATE REQUEST-----",
	"RequestId": "15a735a1-8fe6-45cc-a64c-3c4ff839334e"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|The error message returned because the specified AccessKey ID does not exist. Check whether a valid AccessKey ID is specified when you call the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

