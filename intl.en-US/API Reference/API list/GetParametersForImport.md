# GetParametersForImport {#concept_68621_zh .concept}

Returns the items you need in order to import key material into KMS from your existing key management infrastructure. The returned items are used in the subsequent [ImportKeyMaterial](reseller.en-US/API Reference/API list/ImportKeyMaterial.md#) request.

**Note:** 

-   This CMK’s `Origin` must be `EXTERNAL`.
-   This operation returns a public key, an import token, and the import token expiration time. The public key is base64 encoded. The import token is valid for 24 hours.
-   You must specify the wrapping key \(public key\) type \(RSA\_2048 is supported\) and the wrapping algorithm \(RSAES\_PKCS1\_V1\_5, RSAES\_OAEP\_SHA\_1, and RSAES\_OAEP\_SHA\_256 are supported\).
-   The public key and import token can be used only to encrypt and import the CMK ID specified in this API request.
-   The public key and import token from the same response must be used together.
-   The algorithm used to encrypt the key material must be the one specified in the API request.
-   Each request to this API returns a different pair of public key and import token.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of the CMK. The `Origin` must be `EXTERNAL`.|
|WrappingAlgorithm|String|Yes|The algorithm used to encrypt the key material before importing it.|
|WrappingKeySpec|String|Yes|The type of wrapping key \(public key\) to return in the response.|

## Response parameters { .section}

|Name |Type|Description|
|KeyId|String|The identifier of the CMK to use in a subsequent [ImportKeyMaterial](reseller.en-US/API Reference/API list/ImportKeyMaterial.md#) request.|
|ImportToken|String|The identifier of the CMK to use in a subsequent [ImportKeyMaterial](reseller.en-US/API Reference/API list/ImportKeyMaterial.md#) request.|
|PublicKey|String|The public key to use to encrypt the key material before importing it.|
|TokenExpireTime|String|The time when the import token expires.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GetParametersForImport
&KeyId=<external key id>
&WrappingAlgorithm=<key material encryption algorithm>
&WrappingKeySpec=RSA_2048
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "ImportToken":"ImportToken",
        "PublicKey":"PublicKey",
        "KeyId":"KeyId",
        "TokenExpireTime":"2018-01-25T00:01:02Z",
        "RequestId":"8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc"
}

```

 `XML` format

```
//xml response
<KMS>
  <ImportToken>ImportToken</ImportToken>
  <PublicKey>PublicKey</PublicKey>
  <KeyId>KeyId</KeyId>
  <TokenExpireTime>2018-01-25T00:01:02Z</TokenExpireTime>
  <RequestId>8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc</RequestId>
</KMS>

```

