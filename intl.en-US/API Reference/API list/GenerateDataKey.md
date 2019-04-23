# GenerateDataKey {#concept_28948_zh .concept}

Returns a data encryption key that you can use in your application to encrypt data locally.

This operation returns a plaintext copy of the data key in the `Plaintext` field of the response, and an encrypted copy of the data key in the `CiphertextBlob`field.

**Note:** 

-   We recommend that you use the following pattern to encrypt data locally in your application:
    -   Use this operation \(`GenerateDataKey`\) to get a data encryption key.
    -   Use the plaintext data encryption key \(returned in the `Plaintext` field of the response\) to encrypt data locally, then erase the plaintext data key from memory.
    -   Store the encrypted data key \(returned in the `CiphertextBlob` field of the response\) alongside the locally encrypted data.
-   To decrypt data locally:
    -   Use the [Decrypt](reseller.en-US/API Reference/API list/Decrypt.md#) operation to decrypt the encrypted data key returned by `CiphertextBlob` into a `Plaintext` copy of the data key.
    -   Use the `Plaintext` data key to decrypt data locally, then erase the `Plaintext` data key from memory.
-   When neither `KeySpec` nor `NumberOfBytes` is specified, the default value of `KeySpec` is AES\_256.
-   When both `NumberOfBytes` and `KeySpec` are specified, `NumberOfBytes` prevails.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of CMK. You can user aliases to call this API. For more information, see [Alias Instructions](../../../../reseller.en-US/User Guide/Alias Instructions.md#).|
|KeySpec|String|No|The length and type of the data key. AES\_256 refers to a 256-bit symmetric key. AES\_128 refers to a 128-bit symmetric key.|
|NumberOfBytes|Integer|No|The length of the data key in bytes. Valid value: 1 to 1,024.|
|EncryptionContext|String to string map|No|The json sting of key-value pairs. If you specify this parameter, you need to provide the same parameter when you call `Decrypt`. For more information, see [Encryption Context](../../../../reseller.en-US/User Guide/Encryption Context.md#).|

## Response parameters { .section}

|Name|Type|Description|
|KeyId|String|Globally unique identifier of CMK. If you use an alias in request, the CMK ID of the alias is returned.|
|Plaintext|String|Base64-encoded plaintext key.|
|CiphertextBlob|String|Encrypted data key.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=<cmkid or aliasname>
&KeySpec=AES_256
&EncryptionContext={"Example":"Example"}
&<Common Request Parameters>
			
```

**Response example**

`JSON` format

```
//json response
{
        "CiphertextBlob": "CiphertextBlob",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "Plaintext": "Base64 encoded plaintext",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}

			
```

`XML` format

```
//xml response
<KMS>
        <CiphertextBlob>CiphertextBlob</CiphertextBlob>
        <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
        <Plaintext>Base64 encoded plaintext</Plaintext>
        <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
			
```

