# ImportKeyMaterial {#concept_68622_zh .concept}

When you call [CreateKey](intl.en-US/API Reference/API list/CreateKey.md#) to create a CMK, you can set `Origin` to `EXTERNAL` and do not import the key material. This API is used to import the key material into the CMK.

-   To check the `Origin` of a CMK, call [DescribeKey](intl.en-US/API Reference/API list/DescribeKey.md#).

-   Before calling this API, call [GetParametersForImport](intl.en-US/API Reference/API list/GetParametersForImport.md#) to get the key material ready to import. It returns a public key and an import token. Use the public key to encrypt the key material.


**Note:** 

-   The key material must be a 256-bit symmetric key.
-   You can set the expiration time for the key material, or you can set it to never expire.
-   You can always reimport the same key material and reset the expiration time, but you cannot import a different key material to the specified CMK.
-   After the imported key material expires or is deleted, the specified CMK is unavailable until the same key material are imported again.
-   A key material can be imported to multiple CMKs, but any data or data key encrypted by one CMK cannot be decrypted by another CMK.

## Request parameters { .section}

|Name|Type|Required|Description|
|EncryptedKeyMaterial|String|Yes|Base64-encoded key material to import.|
|ImportToken|String|Yes|The import token you get by calling `GetParametersForImport`.|
|KeyMaterialExpireUnix|Timestamp|No|The time at which the imported key material expires. - If the value is omitted, or is specified as 0, the key material does not expire. - The value cannot be earlier than the timestamp at which you call the API \(Base on the time set on the API server\).|

## Response parameters { .section}

|Name|Type|Description|
|RequestId|String|ID of this request.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=ImportKeyMaterial
&EncryptedKeyMaterial=<your encrypted key material>
&ImportToken=<import token from GetParametersForImport>
&KeyMaterialExpireUnix=1518307200
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
        "RequestId":"ec1017cf-ead4-f3ca-babc-c3b34f3dbecb"
}

```

 `XML` format

```
//xml response
<KMS>
  <RequestId>ec1017cf-ead4-f3ca-babc-c3b34f3dbecb</RequestId>
</KMS>

```

