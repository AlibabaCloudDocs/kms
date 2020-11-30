# Encrypt and decrypt data by using an asymmetric CMK

This topic describes how to use an asymmetric customer master key \(CMK\) to encrypt and decrypt data in Alibaba Cloud CLI.

Asymmetric encryption and decryption generally include the following steps:

1.  An information receiver distributes a public key to a transmitter.
2.  The transmitter uses the public key to encrypt sensitive information.
3.  The transmitter sends the ciphertext generated from the sensitive information to the information receiver.
4.  The receiver uses the private key to decrypt the ciphertext.

## Before you begin

You must call the CreateKey operation to create an asymmetric key in KMS. While you create an asymmetric key, set the KeySpec parameter to a desired key type and the Usage parameter to `ENCRYPT/DECRYPT`. For more information about CreateKey, see [CreateKey](/intl.en-US/API Reference/Key/CreateKey.md).

Create an RSA encryption key.

```
$ aliyun kms CreateKey --KeySpec=RSA_2048 --KeyUsage=ENCRYPT/DECRYPT --ProtectionLevel=HSM
```

## Obtain the public key

1. Call the GetPublicKey operation to obtain the public key of the asymmetric key pair.

```
$ aliyun kms GetPublicKey --KeyId=**** --KeyVersionId=****
```

The following results are returned:

```
{
        "RequestId": "82c383eb-c377-4mf6-bxx8-81hkc1g5g7ab",
        "KeyId": "****",
        "KeyVersionId": "****",
        "PublicKey": "PublicKey-Data****"
}
```

2. Save the public key to the file rsa\_publickey.pub. \(PublicKey-Data\*\*\*\* is a placeholder. You must replace it with the obtained public key.\)

```
$ echo PublicKey-Data**** > rsa_publickey.pub
```

## Use the public key to encrypt data

1. Create a sample plaintext file named plaintext-file.txt that contains "this is plaintext".

```
echo "this is plaintext" > plaintext-file.txt
```

2. Use OpenSSL to encrypt the file and write the obtained binary ciphertext into the plaintext-file.enc file.

```
openssl pkeyutl -encrypt -in plaintext-file.txt \ 
  -inkey rsa_publickey.pub -pubin \
  -pkeyopt rsa_padding_mode:oaep \
  -pkeyopt rsa_oaep_md:sha256 \
  -pkeyopt rsa_mgf1_md:sha256 \
  -out plaintext-file.enc
```

## Call the KMS API to decrypt data

You must call the KMS API and use the private key to decrypt data.

1. Before you transmit the encrypted data over the network, encode it in Base64.

```
$ openssl base64 -in plaintext-file.enc
```

The following Base64-encoded ciphertext is returned:

```
5kdCB06HHeAwgfH9ARY4/9Nv5vlpQ94GXZcmaC9FE59Aw8v8RYdozT6ggSbyZbi+
8STKVq9402MEfmUDmwJLuu0qgAZsCe5wU4JWHh1y84Qn6HT068j0qOy5X2HIlrjs
fCdetgtMtVorSgb3bbERk2RV67nHWrDkecNbUaz+6ik4AlZxv2uWrV62eQ9yUBYm
Jb956LbqnfWdCFxUSHH/qB5QCnLpijzvPmfNlZr653H4nF08gpZjnmlF4FjTu3i2
mGLzK4J3Rh/l7PQHiVMdc4hSnXosg68QmMVdZBGLK9/cD9SYngPDiirU7z0q7Git
dIeloyCAUDFyuQC6a+SqzA==
```

2. Pass the Base64-encoded ciphertext to KMS to decrypt data.

```
aliyun kms AsymmetricDecrypt \
  --KeyId **** \
  --KeyVersionId **** \
  --Algorithm RSAES_OAEP_SHA_256 \
  --CiphertextBlob 5kdCB06HHeAwgfH9ARY4/9Nv5vlpQ94GXZcmaC9FE59Aw8v8RYdozT6ggSbyZbi+8STKVq9402MEfmUDmwJLuu0qgAZsCe5wU4JWHh1y84Qn6HT068j0qOy5X2HIlrjsfCdetgtMtVorSgb3bbERk2RV67nHWrDkecNbUaz+6ik4AlZxv2uWrV62eQ9yUBYmJb956LbqnfWdCFxUSHH/qB5QCnLpijzvPmfNlZr653H4nF08gpZjnmlF4FjTu3i2mGLzK4J3Rh/l7PQHiVMdc4hSnXosg68QmMVdZBGLK9/cD9SYngPDiirU7z0q7GitdIeloyCAUDFyuQC6a+SqzA==
```

The following results are returned:

```
{
        "KeyId": "****",
        "KeyVersionId": "****",
        "Plaintext": "dGhpcyBpcyBwbGFpbnRleHQgDQo=",
        "RequestId": "6be7a8e4-35b9-4549-ad05-c5b1b535a22c"
}
```

3. Decode the returned Base64-encoded plaintext in Base64.

```
echo dGhpcyBpcyBwbGFpbnRleHQgDQo= | openssl base64 -d
```

The following decrypted plaintext is returned:

```
this is plaintext
```

