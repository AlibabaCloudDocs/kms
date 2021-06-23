# AsymmetricEncrypt

Encrypts data by using an asymmetric key.

This operation supports only asymmetric keys for which the **Usage** parameter is set to **ENCRYPT/DECRYPT**. The following table describes the supported encryption algorithms.

|Key type

|Algorithm

|Description

|Maximum length in bytes |
|----------|-----------|-------------|-------------------------|
|RSA\_2048

|RSAES\_OAEP\_SHA\_256

|RSAES-OAEP using SHA-256 and MGF1 with SHA-256

|190 |
|RSA\_2048

|RSAES\_OAEP\_SHA\_1

|RSAES-OAEP using SHA1 and MGF1 with SHA1

|214 |
|RSA\_3072

|RSAES\_OAEP\_SHA\_256

|RSAES-OAEP using SHA-256 and MGF1 with SHA-256

|318 |
|RSA\_3072

|RSAES\_OAEP\_SHA\_1

|RSAES-OAEP using SHA1 and MGF1 with SHA1

|342 |
|EC\_SM2

|SM2PKE

|SM2 elliptic curve public key encryption algorithm

|6047 |

In this example, the asymmetric key whose ID is `5c438b18-05be-40ad-b6c2-3be6752c****` and version ID is `2ab1a983-7072-4bbc-a582-584b5bd8****` and the encryption algorithm `RSAES_OAEP_SHA_1` are used to encrypt the plaintext `SGVsbG8gd29ybGQ=`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=AsymmetricEncrypt&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AsymmetricEncrypt|The operation that you want to perform. Set the value to AsymmetricEncrypt. |
|Algorithm|String|Yes|RSAES\_OAEP\_SHA\_1|The encryption algorithm that you use. |
|KeyId|String|Yes|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The globally unique ID \(GUID\) of the CMK.

 **Note:** You can also set this parameter to an alias that is bound to the CMK. For more information, see [Use aliases](~~68522~~). |
|KeyVersionId|String|Yes|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The ID of the CMK version. The ID must be globally unique. |
|Plaintext|String|Yes|SGVsbG8gd29ybGQ=|The plaintext to be encrypted, which must be Base64-encoded. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The GUID of the CMK.

 **Note:** If you set the KeyId parameter in the request to an alias, the ID of the CMK to which the alias is bound is returned. |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The version of the CMK that is used to encrypt the plaintext. |
|CiphertextBlob|String|BQKP+1zK6+ZEMxTP5qaVzcsgXtWplYBKm0NXdSnB5FzliFxE1bSiu4dnEIlca2JpeH7yz1/S6fed630H+hIH6DoM25fTLNcKj+mFB0Xnh9m2+HN59Mn4qyTfcUeadnfCXSWcGBouhXFwcdd2rJ3n337bzTf4jm659gZu3L0i6PLuxM9p7mqdwO0cKJPfGVfhnfMz+f4alMg79WB/NNyE2lyX7/qxvV49ObNrrJbKSFiz8Djocaf0IESNLMbfYI5bXjWkJlX92DQbKhibtQW8ZOJ//ZC6t0AWcUoKL6QDm/dg5koQalcleRinpB+QadFm894sLbVZ9+N4GVsv1Wbjwg==|The ciphertext.

 **Note:** The value is encoded in Base64. |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|The ID of the request. |

## Examples

Sample requests

```
https://[Endpoint]/?Action=AsymmetricEncrypt
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&Algorithm=RSAES_OAEP_SHA_1
&Plaintext=SGVsbG8gd29ybGQ=
&<Common request parameters>|
```

Sample success responses

`XML` format

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <CiphertextBlob>RKF5WeXJtusIrvuPOjpkA/55EKzi8Wmc/eJ2fQUKphvL750jtInSX1wijw/7jGxUaTHTW6tgIJl2ReN1aI1/wxqGxdzScwsMHxCBncnzQsZF+Fi4UFpI9pr4A1wc2u5Ngwyx9uA4K/kJ5bkS4NvmanxssAPZfSfbJSrAWlCP11tS0Cd54tQVGj4XK9tP9bJDKzKis1NClsOXZtNPX88kUqr3LkgFCsD07IwiePAfI2tn2fzeisje1Q7/d6VkF48c3ZE0DAmnLRujt3yRRGDaKUkI6SUDjuKD4yqBUX15/DKfJtya+JIPQGiO2IEPlhL7+NMT17U0tKtK5ZPNEwxfZw==</CiphertextBlob>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON` format

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "CiphertextBlob": "RKF5WeXJtusIrvuPOjpkA/55EKzi8Wmc/eJ2fQUKphvL750jtInSX1wijw/7jGxUaTHTW6tgIJl2ReN1aI1/wxqGxdzScwsMHxCBncnzQsZF+Fi4UFpI9pr4A1wc2u5Ngwyx9uA4K/kJ5bkS4NvmanxssAPZfSfbJSrAWlCP11tS0Cd54tQVGj4XK9tP9bJDKzKis1NClsOXZtNPX88kUqr3LkgFCsD07IwiePAfI2tn2fzeisje1Q7/d6VkF48c3ZE0DAmnLRujt3yRRGDaKUkI6SUDjuKD4yqBUX15/DKfJtya+JIPQGiO2IEPlhL7+NMT17U0tKtK5ZPNEwxfZw==",
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

