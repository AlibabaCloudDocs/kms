# Generate and verify a digital signature by using an asymmetric CMK

This topic uses Alibaba Cloud CLI as an example to describe how to use an asymmetric customer master key \(CMK\) to generate and verify a digital signature. You can also perform this operation by using the KMS SDK.

Asymmetric encryption generally includes the following steps:

1.  A signer sends a public key to a message receiver.
2.  The signer uses the private key to sign data.
3.  The signer sends the data and signature to the message receiver.
4.  After receiving the data and signature, the message receiver uses the public key to verify the signature.

## Before you begin

You must call the [CreateKey](/intl.en-US/API Reference/Key/CreateKey.md) operation to create an asymmetric key in KMS. While you create an asymmetric key, set the KeySpec parameter to a desired key type and set the Usage parameter to `SIGN/VERIFY`.

-   Create an RSA signature key:

    ```
    aliyun kms CreateKey --KeySpec=RSA_2048 --KeyUsage=SIGN/VERIFY --ProtectionLevel=HSM
    ```

-   Create a NIST P-256 signature key:

    ```
    aliyun kms CreateKey --KeySpec=EC_P256 --KeyUsage=SIGN/VERIFY --ProtectionLevel=HSM
    ```

-   Create a secp256k1 signature key:

    ```
    aliyun kms CreateKey --KeySpec=EC_P256K --KeyUsage=SIGN/VERIFY --ProtectionLevel=HSM
    ```


## Preprocess signature: compute a message digest

Both RSA and ECC signature operations involve first computing the digest of an unsigned message and then signing the digest.

**Note:** The algorithm used to obtain a message digest must match the algorithm used to call KMS to compute a signature. For example, the ECDSA\_SHA\_256 signature algorithm must be used in conjunction with the SHA-256 digest algorithm. It does not support the SHA-384 digest algorithm.

The following example uses the SHA-256 digest algorithm.

1. Save the message "this is message" that needs to be signed into the file message-file.txt:

```
echo "this is message" > message-file.txt
```

2. Compute the SHA-256 digest of the message and save the binary digest to the file message-sha256.bin:

```
openssl dgst -sha256 -binary -out message-sha256.bin  message-file.txt
```

## Call KMS to compute the signature

You must call the KMS API to compute the signature of a message with the private key.

1. Before you transmit the message digest over the network, encode it in Base64.

```
openssl base64 -in message-sha256.bin
```

The following Base64 encoded digest is returned:

```
hRP2cuRFSlfEoUXCGuPyi7kZr18VCTZeVOTw0jbUB6w=
```

2. Pass the Base64 encoded digest to KMS to generate a signature.

**Note:** The parameters passed and the results generated vary depending on key types and signature algorithms. Each signature result generated in the example is stored in a different file.

-   **RSASSA-PSS**

    For RSA keys, you can use the RSASSA-PSS signature algorithm and the SHA-256 digest algorithm to create a signature. Run the following command:

    ```
    aliyun kms AsymmetricSign --KeyId=**** --KeyVersionId=**** \
        --Algorithm=RSA_PSS_SHA_256 --Digest=hRP2cu...
    {
            "KeyId": "****",
            "KeyVersionId": "****",
            "Value": "J7xmdnZ...",
            "RequestId": "70f78da9-c1b6-4119-9635-0ce4427cd424"
    }
    ```

    Decode the signature value in Base64 and generate a binary signature. This signature is saved in the file rsa\_pss\_signature.bin:

    ```
    echo J7xmdnZ... | openssl base64 -d -out rsa_pss_signature.bin
    ```

-   **RSASSA\_PKCS1\_V1\_5**

    For RSA keys, you can use the RSASSA\_PKCS1\_V1\_5 signature algorithm and the SHA-256 digest algorithm to create a signature. Run the following command:

    ```
    aliyun kms AsymmetricSign --KeyId=**** --KeyVersionId=**** \
        --Algorithm=RSA_PKCS1_SHA_256 --Digest=hRP2cu...
    {
            "KeyId": "****",
            "KeyVersionId": "****",
            "Value": "qreBkH/u...",
            "RequestId": "4be57288-f477-4ecd-b7be-ad8688390fbc"
    }
    ```

    Decode the signature value in Base64 and generate a binary signature. This signature is saved in the file rsa\_pkcs1\_signature.bin:

    ```
    echo qreBkH/u... | openssl base64 -d -out rsa_pkcs1_signature.bin
    ```

-   **NIST P-256**

    For NIST curve P-256, you can use the ECDSA signature algorithm and the SHA-256 digest signature to create a signature. Run the following command:

    ```
    aliyun kms AsymmetricSign --KeyId=**** --KeyVersionId=**** \
        --Algorithm=ECDSA_SHA_256 --Digest=hRP2cu...
    {
            "KeyId": "****",
            "KeyVersionId": "****",
            "Value": "MEYCIQD33Y98...",
            "RequestId": "472d789c-d4be-4271-96bb-367f7f0f8ec3"
    }
    ```

    Decode the signature value in Base64 and generate a binary signature. This signature is saved in the file ec\_p256\_signature.bin:

    ```
    echo MEYCIQD33Y98... | openssl base64 -d -out ec_p256_signature.bin
    ```

-   **secp256k1**

    For SECG curve secp256k1, you can use the ECDSA signature algorithm and the SHA-256 digest algorithm to create a signature. Run the following command:

    ```
    aliyun kms AsymmetricSign --KeyId=**** --KeyVersionId=**** \
        --Algorithm=ECDSA_SHA_256 --Digest=hRP2cu...
    {
            "KeyId": "****",
            "KeyVersionId": "****",
            "Value": "MEYCIQDWuuI...",
            "RequestId": "fe41abed-91e7-4069-9f6b-0048f5bf4de5"
    }
    ```

    Decode the signature Value in Base64 and generate a binary signature. This signature is saved in the file ec\_p256k\_signature.bin:

    ```
    echo MEYCIQDWuuI... | openssl base64 -d -out ec_p256k_signature.bin
    ```


## Obtain the public key

Refer to [Obtain the public key](/intl.en-US/Key Service/Key type/Use asymmetric keys/Encrypt and decrypt data by using an asymmetric CMK.md) to obtain the public key of the created asymmetric key pair from the KMS. The preceding example assumes that:

-   The public key of the RSA key pair is saved to the file rsa\_publickey.pub.
-   The public key of the NIST P-256 key pair is saved to the file ec\_p256\_publickey.pub.
-   The public key of the secp256k1 key pair is saved to the file ec\_p256k\_publickey.pub.

## Use the public key to verify the signature

Run the following command lines to verify the signature \(the command varies depending on the algorithm used to generate the public key\):

-   **RSASSA-PSS**

    ```
    openssl dgst \
        -verify rsa_publickey.pub \
        -sha256 \
        -sigopt rsa_padding_mode:pss \
        -sigopt rsa_pss_saltlen:-1 \
        -signature rsa_pss_signature.bin \
        message-file.txt
    ```

-   **RSASSA\_PKCS1\_V1\_5**

    ```
    openssl dgst \
        -verify rsa_publickey.pub \
        -sha256 \
        -signature rsa_pkcs1_signature.bin \
        message-file.txt
    ```

-   **NIST P-256**

    ```
    openssl dgst \
        -verify ec_p256_publickey.pub \
        -sha256 \
        -signature ec_p256_signature.bin \
        message-file.txt
    ```

-   **secp256k1**

    ```
    openssl dgst \
        -verify ec_p256k_publickey.pub \
        -sha256 \
        -signature ec_p256k_signature.bin \
        message-file.txt
    ```


If the verification succeeds, the system displays the following message:

```
Verified OK
```

