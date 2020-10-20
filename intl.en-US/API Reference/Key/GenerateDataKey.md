# GenerateDataKey

Generates a random data key. You can use the data key to encrypt local data.

This operation creates a random data key, encrypts the data key with the specified CMK, and returns the ciphertext and plaintext of the data key. You can use the plaintext to to locally encrypt your data without using KMS and store the ciphertext with the encrypted data. You can obtain the plaintext of the data key by querying the Plaintext value in the response and the ciphertext of the data key by querying the CiphertextBlob value in the response.

The CMK that you specify in the request of this operation is only used to encrypt the data key and is not involved in the generation of the data key. KMS does not record or store the generated data key. Therefore, you need to store the ciphertext of the data key in persistent storage.

We recommend that you encrypt local data by performing the following steps:

-   Call the GenerateDataKey operation.
-   Use the plaintext of the data key that you obtain to encrypt local data in an offline manner and then clear the plaintext of the data key.
-   Store the encrypted data along with the ciphertext of the data key that you obtain.

We recommend that you decrypt local data data by performing the following steps:

-   Call the [Decrypt](~~28950~~) operation to decrypt the locally stored ciphertext of the data key. The plaintext of data key is then returned.
-   Use the plaintext of the data key to decrypt local data in an offline manner and then clear the plaintext of the data key.

## Debugging

[OpenAPI Explorer automatically calculates the signature value. For your convenience, we recommend that you call this operation in OpenAPI Explorer. OpenAPI Explorer dynamically generates the sample code of the operation for different SDKs.](https://api.aliyun.com/#product=Kms&api=GenerateDataKey&type=RPC&version=2016-01-20)

## Request parameters

|Parameter|Type|Required|Example|Description|
|---------|----|--------|-------|-----------|
|Action|String|Yes|GenerateDataKey|The operation that you want to perform. Set the value to GenerateDataKey. |
|KeyId|String|Yes|1234abcd-12ab-34cd-56ef-12345678\*\*\*\*|The globally unique ID of the CMK.

You can also set this parameter to an alias that is bound to the CMK. For more information, see [Use aliases](~~68522~~). |
|KeySpec|String|No|AES\_256|The length of the data key. Valid values:

-   AES\_256: a 256-bit symmetric key
-   AES\_128: a 128-bit symmetric key

**Note:** We recommend that you use the KeySpec or NumberOfBytes parameter to specify the length of a data key. If both parameters are not specified, KMS generates a 256-bit data key. If both parameters are specified, KMS ignores the KeySpec parameter. |
|NumberOfBytes|Integer|No|256|The length of the data key.

Valid values: 1 to 1024.

Unit: bytes. |
|EncryptionContext|Json|No|\{"Example":"Example"\}|A JSON string that consists of key-value pairs. If you specify this parameter, an equivalent value is required when you call the Decrypt operation. For more information, see [EncryptionContext](~~42975~~). |

## Response parameters

|Parameter|Type|Example|Description|
|---------|----|-------|-----------|
|CiphertextBlob|String|ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTSl0oQ|The ciphertext of the data key encrypted by using the primary CMK version. |
|KeyId|String|599fa825-17de-417e-9554-bb032cc6\*\*\*\*|The globally unique ID of the CMK.

**Note:** If you set the KeyId parameter in the request to an alias, the ID of the CMK to which the alias is bound is returned. |
|KeyVersionId|String|2ab1a983-7072-4bbc-a582-584b5bd8\*\*\*\*|The globally unique ID of the CMK version. |
|Plaintext|String|QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0|The plaintext of the data key, which is encoded in Base64. |
|RequestId|String|7021b6ec-4be7-4d3c-8a68-1e85d4d515a0|The ID of the request. |

## Examples

Sample requests

```
https://kms.cn-hangzhou.aliyuncs.com/?Action=GenerateDataKey
&KeyId=1234abcd-12ab-34cd-56ef-12345678****
&<Common request parameters>
```

Sample success responses

`XML` format

```
<KMS>
          <CiphertextBlob>ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTSl0oQ</CiphertextBlob>
          <KeyId>599fa825-17de-417e-9554-bb032cc6****</KeyId>
          <KeyVersionId>2ab1a983-7072-4bbc-a582-584b5bd8****</KeyVersionId>
          <Plaintext>QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0</Plaintext>
          <RequestId>7021b6ec-4be7-4d3c-8a68-1e85d4d515a0</RequestId>
</KMS>
```

`JSON` format

```
{
        "CiphertextBlob": "ODZhOWVmZDktM2QxNi00ODk0LWJkNGYtMWZjNDNmM2YyYWJmS7FmDBBQ0BkKsQrtRnidtPwirmDcS0ZuJCU41xxAAWk4Z8qsADfbV0b+i6kQmlvj79dJdGOvtX69Uycs901qOjop4bTSl0oQ",
        "KeyId": "599fa825-17de-417e-9554-bb032cc6****",
        "KeyVersionId": "2ab1a983-7072-4bbc-a582-584b5bd8****",
        "Plaintext": "QmFzZTY0IGVuY29kZWQgcGxhaW50ZXh0",
        "RequestId": "7021b6ec-4be7-4d3c-8a68-1e85d4d515a0"
}
```

## Error codes

|HttpCode|Error code|Error message|Description|
|--------|----------|-------------|-----------|
|400|Throttling|Request was denied due to request throttling.|The error message returned because your traffic in this period has exceeded the limit. If your business requirements are not met, submit a ticket.|
|404|Forbidden.KeyNotFound|The specified Key is not found.|The error message returned because the specified key does not exist.|

For a list of error codes, visit the [API Error Center](https://error-center.alibabacloud.com/status/product/Kms).

