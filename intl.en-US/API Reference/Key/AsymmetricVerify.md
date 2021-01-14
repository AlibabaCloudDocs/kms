# AsymmetricVerify

Call AsymmetricVerify API to use asymmetric keys for verification.

This operation is only supported for asymmetric keys with **Usage** set to **SIGN/VERIFY**. The following table lists the supported signature algorithms.

|KeySpec

|Algorithm

|Description |
|---------|-----------|-------------|
|RSA\_2048

|RSA\_PSS\_SHA\_256

|RSASSA-PSS using SHA-256 and MGF1 with SHA-256 |
|RSA\_2048

|RSA\_PKCS1\_SHA\_256

|RSASSA-PKCS1-v1\_5 using SHA-256 |
|EC\_P256

|ECDSA\_SHA\_256

|ECDSA on the P-256 Curve\(secp256r1\) with a SHA-256 digest |
|EC\_P256K

|ECDSA\_SHA\_256

|ECDSA on the P-256K Curve\(secp256k1\) with a SHA-256 digest |
|EC\_SM2

|SM2DSA

|SM2 Elliptic Curve Digital Signature Algorithm |

**Note:** According to the national standard GBT32918, when calculating SM2 signature value,**Digest** the parameter is not directly used to calculate the SM3 digest, but for the Z\(A\) the digest computed based on the mosaic values of and M, where M is the original message to be signed and Z\(A\) is A hash value for user A as defined in gbt32918.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=AsymmetricVerify&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AsymmetricVerify|The operation that you want to perform. Set the value to**AsymmetricVerify**. |
|Algorithm|String|Yes|RSA\_PSS\_SHA\_256|The signature algorithm to use. |
|Digest|String|Yes|ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiuyjfzw=|Use**Algorithm**, which is the digest generated for the original message.

**Note:** Use Base64 encoding. |
|KeyId|String|Yes|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The globally unique ID of the CMK.

**Note:** This parameter can also be specified as an alias bound to the master key. For more information, see [use aliases](~~68522~~). |
|KeyVersionId|String|Yes|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The globally unique ID of the CMK version. |
|Value|String|Yes|M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq3a/w==|The signature value to be verified.

**Note:** Use Base64 encoding. |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The globally unique ID of the CMK.

**Note:** If you set the KeyId parameter to the alias of a CMK, the ID of the CMK created by the alias is returned. |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The CMK version used to encrypt the plaintext. |
|Value|Boolean|true|Indicates whether the signature passed the verification. |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|The ID of the request. |

## Examples

Sample requests

```
https://[Endpoint]/?Action=AsymmetricVerify
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&Algorithm=RSA_PSS_SHA_256
&Digest=ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiuyjfzw=
&Value=M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq3a/w==
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <Value>true</Value>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON` format

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "Value": true,
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## Error code

