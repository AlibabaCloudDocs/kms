# CreateCertificate

Creates a certificate.

When you create a certificate, you must specify the type of asymmetric keys, manage the private key in Alibaba Cloud Certificate Manager, and then obtain a certificate signing request \(CSR\). You must submit the CSR to the specified certificate issuing system. The system issues a certificate signed based on the CSR and the associated certificate chain. Then, you must import the certificate and its certificate chain to Alibaba Cloud Certificate Manager.

In this example, the certificate whose ID is `98e85c94-52d0-40c9-b3b2-afda52f4****` is created and a CSR is returned.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CreateCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CreateCertificate|The operation that you want to perform. Set the value to CreateCertificate. |
|KeySpec|String|Yes|RSA\_2048|The type of keys. Valid values:

 -   RSA\_2048
-   EC\_P256
-   EC\_SM2 |
|Subject|String|Yes|CN=userName,OU=kms,O=aliyun,C=CN|The owner of the certificate,

 which is identified in the distinguished name \(DN\) format, as defined in [RFC 2253](https://tools.ietf.org/html/rfc2253?spm=a2c4g.11186623.2.13.265f1a1cGFCn3Q). A DN is a sequence of relative distinguished names \(RDNs\).

 RDNs are key-value pairs in the format of `attribute1=value1,attribute2=value2.` Separate multiple RDNs with commas \(,\). |
|SubjectAlternativeNames|Json|No|\["test1.example.com","test2.example.com"\]|The alias of the certificate owner.

 A domain name list is supported. A maximum of 10 domain names are supported. |
|ProtectionLevel|String|No|SOFTWARE|The protection level for the private key of the certificate. Valid values:

 -   SOFTWARE. This is the default value.
-   HSM

 **Note:** The hardware security module \(HSM\) protection level is available only in the regions where managed HSMs are supported. For more information, see [Regions that support HSMs](~~125803~~). |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:154035569884\*\*\*\*:certificate/98e85c94-52d0-40c9-b3b2-afda52f4\*\*\*\*|The Alibaba Cloud Resource Name \(ARN\). |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Alibaba Cloud Certificate Manager. |
|Csr|String|-----BEGIN CERTIFICATE REQUEST-----MIICxjCCAa4CAQAwPzELMAkGA1UEBhMCQ04xDzANBgNVBAoTBmFsaXl1bjEMMAoGA1UECxMDa21zMREwDwY\*\*\*\*-----END CERTIFICATE REQUEST-----|The CSR returned in the Privacy Enhanced Mail \(PEM\) format. |
|RequestId|String|15a735a1-8fe6-45cc-a64c-3c4ff839334e|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=CreateCertificate
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
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|The error message returned because the AccessKey ID cannot be found. Check whether a valid AccessKey ID is used when you call the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

