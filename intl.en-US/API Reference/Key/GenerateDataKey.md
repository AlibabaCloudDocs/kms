# GenerateDataKey

Generates a random data key that is used to locally encrypt data.

This operation creates a random data key, encrypts the data key by using the specified customer master key \(CMK\), and returns the plaintext and ciphertext of the data key. You can use the plaintext of the data key to locally encrypt data in your own system and store the encrypted data together with the ciphertext of the data key. You can obtain the plaintext of the data key from the Plaintext parameter in the response and the ciphertext of the data key from the CiphertextBlob parameter in the response.

The CMK that you specify in the request of this operation is only used to encrypt the data key and is not involved in the generation of the data key. KMS does not record or store the generated data key. Therefore, you need to store the ciphertext of the data key in persistent storage.

We recommend that you locally encrypt data by performing the following steps:

-   Call the GenerateDataKey operation.
-   Use the plaintext of the data key that you obtain to locally encrypt data in your own system. Then, delete the plaintext of the data key from the memory.
-   Store the encrypted data together with the ciphertext of the data key that you obtain.

We recommend that you locally decrypt data by performing the following steps:

-   Call the [Decrypt](~~28950~~) operation to decrypt the locally stored ciphertext of the data key. The plaintext of the data key is then returned.
-   Use the plaintext of the data key to locally decrypt data and then delete the plaintext of the data key from the memory.

In this example, a random data key is generated for the CMK whose ID is `1234abcd-12ab-34cd-56ef-12345678****`.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GenerateDataKey&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GenerateDataKey|The operation that you want to perform. Set the value to GenerateDataKey. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID \(GUID\) of the CMK.

 You can also set this parameter to an alias that is bound to the CMK. For more information, see [Use aliases](~~68522~~). |
|KeySpec|String|No|AES\_256|The length of the data key to be generated. Valid values:

 -   AES\_256: a 256-bit symmetric key
-   AES\_128: a 128-bit symmetric key

 **Note:** We recommend that you use the KeySpec or NumberOfBytes parameter to specify the length of a data key. If none of the parameters are specified, KMS generates a 256-bit data key. If both parameters are specified, KMS ignores the KeySpec parameter. |
|NumberOfBytes|Integer|No|256|The length of the data key to be generated.

 Valid values: 1 to 1024.

 Unit: bytes. |
|EncryptionContext|Json|No|\{"Example":"Example"\}|A JSON string that consists of key-value pairs. If you specify this parameter, an equivalent value is required when you call the Decrypt operation. For more information, see [EncryptionContext](~~42975~~). |

For more information about common request parameters, see [Common parameters](~~69007~~).

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CiphertextBlob|String|ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS\*\*\*\*|The ciphertext of the data key that is encrypted by using the primary version of the specified CMK. |
|KeyId|String|599fa825-17de-417e-9554-bb032cc6\*\*\*\*|The GUID of the CMK.

 **Note:** If you set the KeyId parameter in the request to an alias of the CMK, the ID of the CMK to which the alias is bound is returned. |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The ID of the CMK version. It is the GUID of the CMK version. |
|Plaintext|String|QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0|The Base64 encoded plaintext of the data key. |
|RequestId|String|7021b6ec-4be7-4d3c-8a68-1e85d4d515a0|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<Common request parameters>|
```

Sample success responses

`XML` format

```
<KMS>
          <CiphertextBlob>ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS****</CiphertextBlob>
          <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
          <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
          <Plaintext>QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0</Plaintext>
          <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
```

`JSON` format

```
{
        "CiphertextBlob": "ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTS****",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
        "Plaintext": "QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}
```

## Error codes

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

