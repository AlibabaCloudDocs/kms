# CertificatePublicKeyVerify

Verifies a digital signature by using a specified certificate.

The signature algorithm in the request parameters must match the key type. The following table describes the mapping between signature algorithms and key types.

|Algorithm

|Key type |
|-----------|----------|
|RSA\_PKCS1\_SHA\_256

|RSA\_2048 |
|RSA\_PSS\_SHA\_256

|RSA\_2048 |
|ECDSA\_SHA\_256

|EC\_P256 |
|SM2DSA

|EC\_SM2 |

In this example, the certificate whose ID is `12345678-1234-1234-1234-12345678****` and the signature algorithm `ECDSA_SHA_256` are used to verify the digital signature `ZOyIygCyaOW6Gj****MlNKiuyjfzw=` of the raw data `VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CertificatePublicKeyVerify&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CertificatePublicKeyVerify|The operation that you want to perform. Set the value to CertificatePublicKeyVerify. |
|Algorithm|String|Yes|ECDSA\_SHA\_256|The signature algorithm. Valid values:

 -   RSA\_PKCS1\_SHA\_256
-   RSA\_PSS\_SHA\_256
-   ECDSA\_SHA\_256
-   SM2DSA

**Note:** The SM2DSA signature algorithm is supported only in regions where managed hardware security modules \(HSMs\) are used in mainland China. For more information, see [Managed HSM overview](~~125803~~). |
|CertificateId|String|Yes|12345678-1234-1234-1234-12345678\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Certificates Manager. |
|Message|String|Yes|VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=|The raw data that is signed.

 The value must be encoded in Base64. For example, if the raw data in the hexadecimal format is `[0x31, 0x32, 0x33, 0x34]`, set this parameter to the Base64-encoded value `MTIzNA==`.

 If the MessageType parameter is set to RAW, the size of the data must be less than or equal to 4 KB.

 If the size of the data is greater than 4 KB, you can set the MessageType parameter to DIGEST and set the Message parameter to the digest of the data. The digest is also called hash value. You can compute the digest of the data on an on-premises machine. Certificates Manager uses the digest that you compute in your own certificate application system. The message digest algorithm that you use must match the specified signature algorithm. Comply with the following mapping between signature algorithms and message digest algorithms:

 -   If the signature algorithm is RSA\_PKCS1\_SHA\_256, RSA\_PSS\_SHA\_256, or ECDSA\_SHA\_256, the message digest algorithm must be SHA-256.
-   If the signature algorithm is SM2DSA, the message digest algorithm must be SM3.

 **Note:** If the key type of the certificate is EC\_SM2 and the MessageType parameter is set to DIGEST, the value of the Message parameter is `e` that is described in GB/T 32918.2-2016 6.1. |
|MessageType|String|Yes|RAW|The type of the message. Valid values:

 -   RAW: the raw data. This is the default value.
-   DIGEST: the message digest \(hash value\) of the raw data. |
|SignatureValue|String|Yes|ZOyIygCyaOW6Gj\*\*\*\*MlNKiuyjfzw=|The signature value.

 The value must be encoded in Base64. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CertificateId|String|12345678-1234-1234-1234-12345678\*\*\*\*|The ID of the certificate. |
|RequestId|String|5979d897-d69f-4fc9-87dd-f3bb73c40b80|The ID of the request. |
|SignatureValid|Boolean|true|The verification result. Valid values:

 -   true: The signature is valid.
-   false: The signature is invalid. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CertificatePublicKeyVerify
&Algorithm=ECDSA_SHA_256
&CertificateId=12345678-1234-1234-1234-12345678****
&Message=VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4=
&MessageType=RAW
&SignatureValue=ZOyIygCyaOW6Gj****MlNKiuyjfzw=
&<Common request parameters>|
```

Sample success responses

`XML` format

```
<KMS>
	  <CertificateId>12345678-1234-1234-1234-12345678****</CertificateId>
	  <SignatureValid>true</SignatureValid>
	  <RequestId>5979d897-d69f-4fc9-87dd-f3bb73c40b80</RequestId>
</KMS>
```

`JSON` format

```
{
  "CertificateId": "12345678-1234-1234-1234-12345678****",
  "SignatureValid": "true",
  "RequestId": "5979d897-d69f-4fc9-87dd-f3bb73c40b80"
}
```

## Error codes

|HTTP status code|Error code|Error message|Description|
|----------------|----------|-------------|-----------|
|404|InvalidAccessKeyId.NotFound|The specified AccessKey ID does not exist.|The error message returned because the specified AccessKey ID does not exist. Check whether a valid AccessKey ID is specified when you call the operation.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

