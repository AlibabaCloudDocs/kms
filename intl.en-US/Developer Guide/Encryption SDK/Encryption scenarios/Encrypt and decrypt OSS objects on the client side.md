# Encrypt and decrypt OSS objects on the client side

If you encrypt or decrypt Object Storage Service \(OSS\) objects on the client side, a data key is generated for each object. This topic describes how to encrypt and decrypt OSS objects on the client side.

## Scenario

If you use a KMS-managed customer master key \(CMK\) to encrypt an object on the client side, you need only to specify the Alibaba Cloud Resource Name \(ARN\) of the CMK when you upload the object. You do not need to provide the client with a data key.

## Encryption mechanism

![OSS](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3996018061/p201595.png)

1.  Obtain a data key.

    Encryption SDK first sends a request to KMS based on the ARN of a CMK to request a data key. KMS generates a random data key and returns the plaintext and ciphertext of the data key.

2.  Encrypt the object and upload it to OSS.

    Encryption SDK receives the plaintext and ciphertext of the data key from KMS and uses the plaintext of the data key to encrypt the object on the client side. Then, Encryption SDK encapsulates the ciphertext of the data key in a message header, stores the message header as the metadata of the object, and uploads the encrypted object to OSS.


## Decryption mechanism

1.  Download the object.

    Encryption SDK downloads the encrypted object and the message header stored as metadata from the OSS server, and parses the message header to obtain the encrypted data key.

2.  Decrypt the object.

    Encryption SDK parses the CMK ARN to obtain information about the region and sends the ciphertext of the data key to the KMS server in the specific region. KMS uses the CMK to decrypt the ciphertext of the data key and returns the plaintext of the data key to the client where the object is encrypted. Encryption SDK uses the plaintext of the data key to decrypt the encrypted object and obtain the original object.


**Note:** You can use Galois/Counter Mode \(GCM\) to encrypt a data object. In this mode, you can decrypt all the encrypted data or only a specific segment of the data. If you decrypt all the encrypted data, data integrity is verified. Decrypted data is returned only after the data passes the verification. If you decrypt only a specific segment of the data, data integrity is not verified.

## Sample code

You can obtain the sample code from [OSSEncryption](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/oss/OSSEncryptionSample.java).

