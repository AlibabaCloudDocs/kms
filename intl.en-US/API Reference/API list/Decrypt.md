# Decrypt {#concept_28950_zh .concept}

Decrypts the ciphertext in `CiphertextBlob`.

Ciphertext can be generated by the following APIs:

-   [GenerateDataKey](reseller.en-US/API Reference/API list/GenerateDataKey.md#) 
-    [Encrypt](reseller.en-US/API Reference/API list/Encrypt.md#) 

## Request parameters { .section}

|Name|Type|Required|Description|
|CiphertextBlob|String|Yes|Ciphertext to be decrypted.|
|EncryptionContext|String|No|JSON string of key-value pairs. If you specify this parameter in the `Encrypt` or `GenerateDataKey` API, you need to provide the same parameter before you can decrypt the ciphertext. For more information, see [Encryption Context](../../../../../reseller.en-US/User Guide/Encryption Context.md#).|

## Response parameters { .section}

|Name|Type|Description|
|KeyId|String|Globally unique identifier of CMK. ID of the CMK used by the encrypted ciphertext.|
|Plaintext|String|Decrypted plaintext.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=Decrypt
&CiphertextBlob=<your ciphertextblob>
&EncryptionContext={"Example":"Example"}
&<Common Request Parameters>

```

**Response example**

`JSON` format

```
//json response
{
"KeyId": "202b9877-5a25-46e3-a763-e20791b5****"
"Plaintext": "Plaintext"
"RequestId": "207596a2-36d3-4840-b1bd-f87044699bd7"
}

```

 `XML` format

```
//xml response
<KMS>
        <KeyId>202b9877-5a25-46e3-a763-e20791b5****</KeyId>
        <Plaintext>Plaintext</Plaintext>
        <RequestId>4bd560a1-729e-45f1-a3d9-b2a33d61046b</RequestId>
</KMS>


```
