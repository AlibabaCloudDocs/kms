# How Encryption SDK works

This topic describes how Encryption SDK works to help you better use Encryption SDK to encrypt data, decrypt data, generate signatures, and verify signatures.

## Encryption and decryption

-   Encryption

    Encryption SDK uses digital envelopes to encrypt data. Envelope encryption allows you to use customer master keys \(CMKs\) of KMS to encrypt data keys and use data keys to encrypt data. For more information about envelope encryption, see [What is envelope encryption?](/intl.en-US/FAQ/What is envelope encryption?.md)

    ![Encryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5086018061/p201590.png)

    1.  Call the [GenerateDataKey](/intl.en-US/API Reference/Key/GenerateDataKey.md) operation to generate a random data key. The plaintext and ciphertext of the data key are returned.
    2.  Use the data key to encrypt data and obtain ciphertext data.
    3.  Encode the ciphertext data key and ciphertext data to generate an encryption message.
-   Decryption

    ![Decryption](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5086018061/p201591.png)

    1.  Call the [Decrypt](/intl.en-US/API Reference/Key/Decrypt.md) operation to obtain the plaintext of the data key.
    2.  Use the data key to decrypt the ciphertext data and obtain the plaintext.

## Signature generation and verification

Encryption SDK can use asymmetric keys to sign data and verify generated signatures. The RSA, ECC, and SM2 asymmetric key algorithms are supported. For more information, see [Overview](/intl.en-US/Key service/Key type/Use asymmetric keys/Overview.md).

Signature generation and verification process:

1.  A signer sends a public key to a message receiver.
2.  The signer uses the private key that matches the public key to sign data.
3.  The signer sends the data and signature to the message receiver.
4.  The message receiver uses the public key to verify the received signature.

Digital signatures are widely used to defend against data tampering and authenticate identities.

-   You can use digital signatures to protect the integrity of your binary code and verify that the code has not been tampered with. This helps provide a trusted execution environment.
-   Digital signatures can also be used in digital certificate systems. In such a system, a certificate authority \(CA\) provides a signature for a digital certificate to certify the entity information, public and private key information, key purpose, expiration date, and issuer. The private key holder of a certificate uses their private key to sign a message. The message receiver uses the public key contained in the certificate to verify the message signature and uses the public key of the certificate issuer to verify the certificate.

**Note:** For more information about CMKs, data keys, ciphertext data keys, ciphertext data, and EncryptionContext, see [Terms](/intl.en-US/Product Introduction/Terms.md).

