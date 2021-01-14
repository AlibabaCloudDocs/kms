# GetParametersForImport

Queries the GetParametersForImport of CMK materials.

The returned parameters can be used to perform the [ImportKeyMaterial](~~68621~~).

**Note:**

-   The CMK material must be external, that is**Origin** for**EXTERNAL**.
-   The type of the public key used to encrypt the key material must be specified, and the encryption algorithm must be specified. See the following table for details.
-   This operation returns a public key \(PublicKey\), an import token, and the import token expiration time. The public key is base64 encoded. The token is valid for 24 hours.
-   The public key and STS token can be used only for the CMK specified in this request.
-   The public key and token that are returned from the same response must be used together.
-   The algorithm used to encrypt the key material must be the one specified in the API request.
-   Each call returns a public key that is different from the token.

|Types of public keys

|Encryption Algorithm

|Description |
|----------------------|----------------------|-------------|
|RSA\_2048

|RSAES\_PKCS1\_V1\_5

RSAES\_OAEP\_SHA\_1

RSAES\_OAEP\_SHA\_256

|It supports keys of any protection level in all regions. |
|EC\_SM2

|SM2PKE

|Only the protection level is **HSM** with the hardware security module detection type **commercial password testing and authentication by State Security Bureau**\(For more information, see [overview of managed hardware security module](~~125803~~)\). |

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GetParametersForImport&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GetParametersForImport|The operation that you want to perform. Set the value to**GetParametersForImport**. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique identifier of the CMK.

**Note:** The key material source must be external \(**Origin** for**EXTERNAL**\). |
|WrappingAlgorithm|String|Yes|RSAES\_PKCS1\_V1\_5|The algorithm used to encrypt the key material. |
|WrappingKeySpec|String|Yes|RSA\_2048|The type of the public key used to encrypt the key material. |

## Response parameters

|Prameter|Type|Sample response|Description|
|--------|----|---------------|-----------|
|ImportToken|String|Base64String|Import token.

Subsequent calls [ImportKeyMaterial](~~68622~~) required. |
|KeyId|String|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique identifier of the CMK.

Subsequent calls [ImportKeyMaterial](~~68622~~) required. |
|PublicKey|String|MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB|The public key used to encrypt the key material. |
|RequestId|String|8 cdf51 fd-bcd6-d79a-0ef4-e52c9b5466dc|The ID of the request. |
|TokenExpireTime|String|2018-01-25T00:01:02Z|The time when the import token expires. |

## Examples

Sample requests

```
https://[Endpoint]/? Action=GetParametersForImport
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&WrappingAlgorithm=RSAES_PKCS1_V1_5
&WrappingKeySpec=RSA_2048
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <ImportToken>Base64String</ImportToken>
    <PublicKey>MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB</PublicKey>
    <KeyId>KeyId</KeyId>
    <TokenExpireTime>2018-01-25T00:01:02Z</TokenExpireTime>
    <RequestId>8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc</RequestId>
</KMS>
```

`JSON` format

```
{
        "ImportToken":"Base64String",
        "PublicKey":"MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAlls4uIBxD0GG84C+lGBO6Dhpf1J3XimC6cPmPNaKKJMOzoX4tD+C+r7aZv8lZ3vnPfxuxvy/YwG+whUxTEEFUdqJTOIzhPfYucupqKM92crVHIuG+xtMVeHKjyTr+UrtKCsQikqHT+19yDRN/RMoo2HUx0gmEnRyXd8t3JyUXun9FdoxKA08GrsV7nodb9ZsoBLhnev7tTLcXvLyKW6XG1ZQCQm6dPnbnwLeDXR7uK0Lqn9PM28mBIdaiQUQxj2XbM1CoJA+JiyVX3Ptdb+4rqukb4Rb05B80Bs9xV/cf7FIku08l7xGhrGiQFq+DFXwQWtwihXHZxz3LhldU+4ZPwIDAQAB",
        "KeyId":"KeyId",
        "TokenExpireTime":"2018-01-25T00:01:02Z",
        "RequestId":"8cdf51fd-bcd6-d79a-0ef4-e52c9b5466dc"
}
```

## Error codes

