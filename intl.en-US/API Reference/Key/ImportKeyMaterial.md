# ImportKeyMaterial

Call the ImportKeyMaterial operation to import the key material.

Call [CreateKey](~~28947~~) when creating a CMK, you can select its key material source as external.**Origin** set to**EXTERNAL**. This API is used to import the key material into the CMK.

-   To view the CMK**Origin**, see [DescribeKey](~~28952~~).
-   Before importing key material, you need to call the [GetParametersForImport](~~68621~~) obtain the parameters required to import the key material, including the public key and import token.

**Note:**

-   The key type of the pair is**Aliyun\_AES\_256** the key material must be 256 bits. The key type must be**Aliyun\_SM4** the CMK and key material must be 128 bits.
-   You can set the expiration time for the key material, or you can set it to never expire.
-   You can reimport the key material and reset the expiration time for the specified CMK at any time, but the same key material must be imported.
-   After the imported key material expires or is deleted, the specified CMK is unavailable until the same key material are imported again.
-   A Key material can be imported to multiple cmks, but any Data or Data Key encrypted by one CMK cannot be decrypted by another CMK.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=ImportKeyMaterial&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|ImportKeyMaterial|The operation that you want to perform. Set the value to**ImportKeyMaterial**. |
|EncryptedKeyMaterial|String|Yes|bCPZx7I6v6KXsqEpr2OXKxuj2CCRtKdwp75Bw+BGncYqBdfjFBYRtOE6HRlT0oeiRDWzwnw9OA54OL36smDJrq4Lo9x0CyYDiuKnRkcKtMtlzW0din7Pd7IlZWWRdVueiw2qpzl7PkUWQGTdsdbzpfJJQ+qj/cRIrk/E83UGyeyytSpgnb+lu0xEYcPajRyWNsbi98N3pqqQzHXNNHO2NJqHlnQgglqTiBEjkGeKFhfKmTc3vjulIdVa3EaVIN6lwWfgx+UUYSrvbA77WDYKlDsZ4SbK2/T7za9Tp1qU7Ynqba7OKGVVj7PMbiaO80AxWZnjUMYCgEp5w7V+seOXqw==|Use**GetParametersForImport** the Returned public key and the base64-encoded key material. |
|ImportToken|String|Yes|Base64String|By calling**GetParametersForImport** the import token. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The ID of the CMK to be imported. |
|KeyMaterialExpireUnix|Long|Yes|0|The time when the key material expires.

If this parameter is not specified or set this parameter to 0, the key material does not expire.

**Note:** The value cannot be earlier than the time when the API is called \(based on the server time\). |

## Response parameters

|Prameter|Type|Sample response|Description|
|--------|----|---------------|-----------|
|RequestId|String|ec1017 cf-ead4-f3ca-babc-c3b34f3dbecb|The ID of the request. |

## Examples

Sample requests

```
https://[Endpoint]/? Action=ImportKeyMaterial
&EncryptedKeyMaterial=bCPZx7I6v6KXsqEpr2OXKxuj2CCRtKdwp75Bw+BGncYqBdfjFBYRtOE6HRlT0oeiRDWzwnw9OA54OL36smDJrq4Lo9x0CyYDiuKnRkcKtMtlzW0din7Pd7IlZWWRdVueiw2qpzl7PkUWQGTdsdbzpfJJQ+qj/cRIrk/E83UGyeyytSpgnb+lu0xEYcPajRyWNsbi98N3pqqQzHXNNHO2NJqHlnQgglqTiBEjkGeKFhfKmTc3vjulIdVa3EaVIN6lwWfgx+UUYSrvbA77WDYKlDsZ4SbK2/T7za9Tp1qU7Ynqba7OKGVVj7PMbiaO80AxWZnjUMYCgEp5w7V+seOXqw==
&ImportToken=Base64String
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&KeyMaterialExpireUnix=0
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
    <RequestId>ec1017cf-ead4-f3ca-babc-c3b34f3dbecb</RequestId>
</KMS>
```

`JSON` format

```
{
        "RequestId":"ec1017cf-ead4-f3ca-babc-c3b34f3dbecb"
}
```

## Error codes

