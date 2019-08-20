# Encrypt {#concept_28949_zh .concept}

Encrypts plaintext into ciphertext by using a CMK.

-   You can encrypt up to 6 KB of arbitrary data, such as an RSA key, a database password, or other sensitive information.
-   To move encrypted data from one region to another, you can use this API to encrypt in the new region the plaintext data key that was used to encrypt the data in the original region. An encrypted data key is generated in the new region. You can [Decrypt](reseller.en-US/API Reference/API list/Decrypt.md#) the data key in the new region.

## Request parameters { .section}

|Name|Type|Required|Description|
|KeyId|String|Yes|Globally unique identifier of CMK. You can user aliases to call this API. For more information, see [Alias Instructions](../../../../../reseller.en-US/User Guide/Alias Instructions.md#).|
|Plaintext|String|Yes|Plaintext to be encrypted. The value is Base64-encoded.|
|EncryptionContext|String to string map|No|The JSON string of key-value pairs. If you specify this parameter, you need to provide the same parameter when you call `Decrypt`. For more information, see [Encryption Context](../../../../../reseller.en-US/User Guide/Encryption Context.md#).|

## Response parameters { .section}

|Name |Type|Description|
|KeyId|String|Globally unique identifier of CMK. If you use an alias in request, the CMK ID of the alias is returned.|
|CiphertextBlob|String|Encrypted ciphertext.|

## Examples { .section}

**Request example**

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=Encrypt
&KeyId=<cmkid or aliasname>
&Plaintext=<data need encrypt>
&EncryptionContext={"Example":"Example"}
&<Common Request Parameters>

```

**Response example**

 `JSON` format

```
//json response
{
	"KeyId": "your-key-id",
	"CiphertextBlob": "CiphertextBlob",
	"RequestId": "475f1620-b9d3-4d35-b5c6-3fbdd941423d"
}

```

 `XML` format

```
//xml response
<KMS>
	<KeyId>your-key-id</KeyId>
	<CiphertextBlob>CiphertextBlob</CiphertextBlob>
	<RequestId>475f1620-b9d3-4d35-b5c6-3fbdd941423d</RequestId>
</KMS>


```

