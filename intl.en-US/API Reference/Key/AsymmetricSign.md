# AsymmetricSign

Generates a digital signature by using an asymmetric key.

This operation supports only asymmetric keys for which the **Usage** parameter is set to **SIGN/VERIFY**. The following table describes the supported signature algorithms.

|Key type

|Algorithm

|Description |
|----------|-----------|-------------|
|RSA\_2048

|RSA\_PSS\_SHA\_256

|RSASSA-PSS using SHA-256 and MGF1 with SHA-256 |
|RSA\_2048

|RSA\_PKCS1\_SHA\_256

|RSASSA-PKCS1-v1\_5 using SHA-256 |
|RSA\_3072

|RSA\_PSS\_SHA\_256

|RSASSA-PSS using SHA-256 and MGF1 with SHA-256 |
|RSA\_3072

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

|SM2 elliptic curve public key encryption algorithm |

**Note:** When you calculate the SM2 signature based on GB/T 32918, the **Digest** parameter is used to calculate the digest value of the combination of Z\(A\) and M, rather than the SM3 digest value. M indicates the original message to be signed. Z\(A\) indicates the hash value for User A. The hash value is defined in GB/T 32918.

In this example, the asymmetric key whose ID is `5c438b18-05be-40ad-b6c2-3be6752c****` and version ID is `2ab1a983-7072-4bbc-a582-584b5bd8****` and the signature algorithm `RSA_PSS_SHA_256` are used to generate a digital signature for the digest `ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiuy****=`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=AsymmetricSign&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|AsymmetricSign|The operation that you want to perform. Set the value to AsymmetricSign. |
|Algorithm|String|Yes|RSA\_PSS\_SHA\_256|The signature algorithm. |
|Digest|String|Yes|ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiu\*\*\*\*=|The digest that is generated for the original message by using a hash algorithm. The hash algorithm is specified by the Algorithm parameter.

 **Note:** The value must be encoded in Base64. |
|KeyId|String|Yes|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The globally unique ID \(GUID\) of the CMK.

 **Note:** You can also set this parameter to an alias that is bound to the CMK. For more information, see [Use aliases](~~68522~~). |
|KeyVersionId|String|Yes|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The ID of the CMK version. The ID must be globally unique. |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|KeyId|String|5c438b18-05be-40ad-b6c2-3be6752c\*\*\*\*|The GUID of the CMK.

 **Note:** If you set the KeyId parameter in the request to an alias, the ID of the CMK to which the alias is bound is returned. |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The ID of the CMK version. It is the GUID of the CMK version. |
|Value|String|M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq\*\*\*\*==|The calculated signature.

 **Note:** The value is encoded in Base64. |
|RequestId|String|475f1620-b9d3-4d35-b5c6-3fbdd941423d|The ID of the request. |

## Examples

Sample requests

```
http(s)://[Endpoint]/?Action=AsymmetricSign
&Algorithm=RSA_PSS_SHA_256
&Digest=ZOyIygCyaOW6GjVnihtTFtIS9PNmskdyMlNKiu****=
&KeyId=5c438b18-05be-40ad-b6c2-3be6752c****
&KeyVersionId=2ab1a983-7072-4bbc-a582-584b5bd8****
&<Common request parameters>|
```

Sample success responses

`XML` format

```
<KMS>
    <KeyId>5c438b18-05be-40ad-b6c2-3be6752c****</KeyId>
    <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
    <Value>M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq****==</Value>
    <RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>
```

`JSON` format

```
{
  "KeyId": "5c438b18-05be-40ad-b6c2-3be6752c****",
  "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
  "Value": "M2CceNZH00ZgL9ED/ZHFp21YRAvYeZHknJUc207OCZ0N9wNn9As4z2bON3FF3je+1Nu+2+/8Zj50HpMTpzYpMp2R93cYmACCmhaYoKydxylbyGzJR8y9likZRCrkD38lRoS40aBBvv/6iRKzQuo9EGYVcel36cMNg00VmYNBy3pa1rwg3gA4l3cy6kjayZja1WGPkVhrVKsrJMdbpl0ApLjXKuD8rw1n1XLCwCUEL5eLPljTZaAveqdOFQOiZnZEGI27qIiZe7I1fN8tcz6anS/gTM7xRKE++5egEvRWlTQQTJeApnPSiUPA+8ZykNdelQsOQh5SrGoyI4A5pq****==",
  "RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

