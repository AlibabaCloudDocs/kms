# DescribeCertificate

Queries information about a certificate.

In this example, the information about the certificate whose ID is `9a28de48-8d8b-484d-a766-dec4****` is queried. The certificate information includes the certificate ID, creation time, certificate issuer, validity period, serial number, and signature algorithm.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=DescribeCertificate&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|DescribeCertificate|The operation that you want to perform. Set the value to DescribeCertificate. |
|CertificateId|String|Yes|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Alibaba Cloud Certificate Manager. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|Arn|String|acs:kms:cn-hangzhou:159498693826\*\*\*\*:certificate/9a28de48-8d8b-484d-a766-dec4\*\*\*\*"|The Alibaba Cloud Resource Name \(ARN\). |
|CertificateId|String|9a28de48-8d8b-484d-a766-dec4\*\*\*\*|The ID of the certificate. It is the GUID of the certificate in Alibaba Cloud Certificate Manager. |
|CreatedAt|String|2020-10-13T03:05:03Z|The time when the certificate was created. |
|Issuer|String|CN=testCA,OU=kms,O=aliyun,C=CN|The issuer of the certificate, which is identified in the distinguished name \(DN\) format. |
|KeySpec|String|RSA\_2048|The name of the asymmetric algorithm used by the certificate. |
|NotAfter|String|2022-10-13T03:09:00Z|The end of the validity period of the certificate. |
|NotBefore|String|2020-10-13T03:09:00Z|The beginning of the validity period of the certificate. |
|ProtectionLevel|String|SOFTWARE|The protection level for the private key of the certificate. Valid values:

 -   SOFTWARE. This is the default value.
-   HSM

**Note:** The hardware security module \(HSM\) protection level is available only in the regions where managed HSMs are supported. For more information, see [Regions that support HSMs](~~125803~~). |
|RequestId|String|edb671a3-c5a1-4ebe-a1de-d748b640bdf2|The ID of the request. |
|Serial|String|12345678|The serial number of the certificate. |
|SignatureAlgorithm|String|ECDSA-SHA256|The signature algorithm of the certificate. Valid values:

 -   RSA2048-SHA256
-   ECDSA-SHA256
-   SM2-SM3 |
|Status|String|ACTIVE|The status of the certificate. Valid values:

 -   PENDING: The certificate is to be imported.
-   ACTIVE: The certificate is enabled.
-   DISABLE: The certificate is disabled.
-   REVOKED: The certificate is revoked. |
|Subject|String|CN=userName,OU=aliyun,O=aliyun,C=CN|The owner of the certificate, which is identified in the DN format. |
|SubjectAlternativeNames|List|\["test1.example.com","test2.example.com"\]|The alias of the certificate owner.

 A domain name list is supported. A maximum of 10 domain names are supported. |
|SubjectKeyIdentifier|String|79 36 26 DE 9F F5 15 E3 56 DC \*\*\*\*|The public key identifier of the certificate owner. |
|SubjectPublicKey|String|-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----|The public key in the certificate. |
|Tags|Map|\[\{"key1":"value"\},"key2":"value2"\]|The tag of the certificate. |
|UpdatedAt|String|2020-12-23T06:10:13Z|The time when the certificate was updated. |

## Examples

Sample requests

```
http(s)://[Endpoint]/? Action=DescribeCertificate
&CertificateId=9a28de48-8d8b-484d-a766-dec4****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
	  <Status>ACTIVE</Status>
	  <ProtectionLevel>SOFTWARE</ProtectionLevel>
	  <RequestId>edb671a3-c5a1-4ebe-a1de-d748b640bdf2</RequestId>
	  <Issuer>CN=testCA,OU=kms,O=aliyun,C=CN</Issuer>
	  <CertificateId>9a28de48-8d8b-484d-a766-dec4****</CertificateId>
	  <CreatedAt>2020-10-13T03:05:03Z</CreatedAt>
	  <KeySpec>RSA_2048</KeySpec>
	  <SubjectAlternativeNames>[\"test1.example.com\",\"test2.example.com\"]</SubjectAlternativeNames>
	  <SignatureAlgorithm>ECDSA-SHA256</SignatureAlgorithm>
	  <SubjectKeyIdentifier>79 36 26 DE 9F F5 15 E3 56 DC ********</SubjectKeyIdentifier>
	  <NotAfter>2022-10-13T03:09:00Z</NotAfter>
	  <UpdatedAt>2020-10-13T03:15:00Z</UpdatedAt>
	  <Subject>CN=userName,OU=aliyun,O=aliyun,C=CN</Subject>
	  <Serial>12345678</Serial>
	  <SubjectPublicKey>-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----</SubjectPublicKey>
	  <NotBefore>2020-10-13T03:09:00Z</NotBefore>
	  <Arn>acs:kms:cn-hangzhou:159498693826****:certificate/9a28de48-8d8b-484d-a766-dec4****</Arn>
	  <Tags>[{\"key1\":\"value\"},\"key2\":\"value2\"]</Tags>
</KMS>
```

`JSON` format

```
{
    "Status": "ACTIVE",
    "ProtectionLevel": "SOFTWARE",
    "RequestId": "edb671a3-c5a1-4ebe-a1de-d748b640bdf2",
    "Issuer": "CN=testCA,OU=kms,O=aliyun,C=CN",
    "CertificateId": "9a28de48-8d8b-484d-a766-dec4****",
    "CreatedAt": "2020-10-13T03:05:03Z",
    "KeySpec": "RSA_2048",
    "SubjectAlternativeNames": "[\"test1.example.com\",\"test2.example.com\"]",
    "SignatureAlgorithm": "ECDSA-SHA256",
    "SubjectKeyIdentifier": "79 36 26 DE 9F F5 15 E3 56 DC ********",
    "NotAfter": "2022-10-13T03:09:00Z",
    "UpdatedAt": "2020-10-13T03:15:00Z",
    "Subject": "CN=userName,OU=aliyun,O=aliyun,C=CN",
    "Serial": "12345678",
    "SubjectPublicKey": "-----BEGIN PUBLIC KEY----- MIIBIjA -----END PUBLIC KEY-----",
    "NotBefore": "2020-10-13T03:09:00Z",
    "Arn": "acs:kms:cn-hangzhou:159498693826****:certificate/9a28de48-8d8b-484d-a766-dec4****",
    "Tags": "[{\"key1\":\"value\"},\"key2\":\"value2\"]"
 }
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|Certificate.NotFound|The specified certificate is not found.|The error message returned because the specified certificate does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

