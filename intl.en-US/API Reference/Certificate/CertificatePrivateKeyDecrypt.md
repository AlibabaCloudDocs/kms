# CertificatePrivateKeyDecrypt

Decrypts data by using a specific certificate.

Limit: The encryption algorithm in the request parameters must match the key type.

The following table describes the mapping between encryption algorithms and key types.

|Algorithm

|Key Type |
|-----------|----------|
|RSAES\_OAEP\_SHA\_1

|RSA\_2048 |
|RSAES\_OAEP\_SHA\_256

|RSA\_2048 |
|SM2PKE

|EC\_SM2 |

In this example, the certificate whose ID is `12345678-1234-1234-1234-12345678****` and the encryption algorithm `RSAES_OAEP_SHA_256` are used to decrypt the data `ZOyIygCyaOW6Gj****MlNKiuyjfzw=`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=CertificatePrivateKeyDecrypt&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|CertificatePrivateKeyDecrypt|The operation that you want to perform. Set the value to CertificatePrivateKeyDecrypt. |
|Algorithm|String|Yes|RSAES\_OAEP\_SHA\_256|The encryption algorithm. Valid values:

-   RSAES\_OAEP\_SHA\_1
-   RSAES\_OAEP\_SHA\_256
-   SM2PKE

**Note:** The SM2PKE encryption algorithm is supported only in regions in mainland China. In these regions, managed hardware security modules \(HSMs\) are used. For more information, see [Overview of managed HSM](~~125803~~). |
|CertificateId|String|Yes|12345678-1234-1234-1234-12345678\*\*\*\*|The ID of the certificate. It is the globally unique identifier \(GUID\) of the certificate in Certificates Manager. |
|CiphertextBlob|String|Yes|ZOyIygCyaOW6Gj\*\*\*\*MlNKiuyjfzw=|The data that you want to decrypt.

The value must be encoded in Base64. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CertificateId|String|12345678-1234-1234-1234-12345678\*\*\*\*|The ID of the certificate. |
|Plaintext|String|VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4|The plaintext after data is decrypted.

The value is encoded in Base64. |
|RequestId|String|5979d897-d69f-4fc9-87dd-f3bb73c40b80|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=CertificatePrivateKeyDecrypt
&Algorithm=RSAES_OAEP_SHA_256
&CertificateId=12345678-1234-1234-1234-12345678****
&CiphertextBlob=ZOyIygCyaOW6Gj****MlNKiuyjfzw=
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
        <CertificateId>12345678-1234-1234-1234-12345678****</CertificateId>
        <Plaintext>VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4</Plaintext>
        <RequestId>5979d897-d69f-4fc9-87dd-f3bb73c40b80</RequestId>
</KMS>
```

`JSON` format

```
{
  "CertificateId": "12345678-1234-1234-1234-12345678****",
  "Plaintext": "VGhlIHF1aWNrIGJyb3duIGZveCBqdW1wcyBvdmVyIHRoZSBsYXp5IGRvZy4",
  "RequestId": "5979d897-d69f-4fc9-87dd-f3bb73c40b80"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|404|Certificate.NotFound|The specified certificate is not found.|The error message returned because the specified certificate does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

