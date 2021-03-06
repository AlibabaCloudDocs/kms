# Overview

Unlike symmetric keys, asymmetric keys are used to verify digital signatures or encrypt sensitive information between systems with different trust levels.

An asymmetric key pair consists of a public key and a private key, which are cryptographically related to each other. The public key is available for all to use, but the private key must be kept secure and used only by trusted users. Alibaba Cloud supports popular asymmetric key algorithms and provides sufficient security strength to ensure the security of encrypted data and digital signatures.

Key Management Service \(KMS\) generates a certificate signing request \(CSR\) file for an asymmetric customer master key \(CMK\). A certificate applicant submits the CSR file to a certificate authority \(CA\). Then, the CA sends back a digital certificate that is signed by using the private key of the CA. The digital certificate can be used to ensure the security of emails, terminals, code signing, trusted website services, and identity authorization management systems.

## Types of asymmetric keys

The following table describes the types of asymmetric keys that KMS supports.

|Algorithm|Key type|Description|Purpose|
|---------|--------|-----------|-------|
|RSA|-   RSA\_2048
-   RSA\_3072

|RSA asymmetric cryptosystem|-   Encrypt or decrypt data.
-   Generate a digital signature. |
|ECC|-   EC\_P256: National Institute of Standards and Technology \(NIST\)-recommended elliptic curve P-256
-   EC\_P256K: Standards for Efficient Cryptography Group \(SECG\) elliptic curve secp256k1

|Elliptic-curve cryptography \(ECC\)|Generate a digital signature.|
|SM2|EC\_SM2|ECC defined by GB/T 32918|-   Encrypt or decrypt data.
-   Generate a digital signature. |

## Data encryption

In data encryption, asymmetric keys are used to transmit sensitive information. The following operations describe a typical scenario:

1.  An information receiver distributes a public key to a transmitter.
2.  The transmitter uses the public key to encrypt sensitive information.
3.  The transmitter sends the ciphertext generated from the sensitive information to the information receiver.
4.  The information receiver uses the private key to decrypt the ciphertext.

The private key can be used only by the information receiver. This ensures that the plaintext of sensitive information cannot be intercepted and decrypted by unauthorized parties during transmission. This encryption method is widely used to exchange keys. For example, session keys are exchanged in Transport Layer Security \(TLS\) handshakes, and encryption keys are exported and imported between different hardware security modules \(HSMs\).

For more information, see [Encrypt and decrypt data by using an asymmetric CMK](/intl.en-US/Key Service/Key type/Use asymmetric keys/Encrypt and decrypt data by using an asymmetric CMK.md).

## Digital signatures

Asymmetric keys are also used to generate digital signatures. Private keys can be used to sign messages or information. Private keys are strictly protected and can be used only by trusted users to generate signatures. After a signature is generated, you can use the corresponding public key to verify the signature to achieve the following purposes:

-   Verify data integrity. If the data does not match its signature, the data may be tampered with.
-   Verify message authenticity. If a message does not match its signature, the message transmitter does not hold the private key.
-   Provide non-repudiation for signatures. If the data matches its signature, the signer cannot deny this signature.

The following operations describe a typical signature verification scenario:

1.  A signer sends a public key to a receiver.
2.  The signer uses the private key that matches the public key to sign data.
3.  The signer sends the data and signature to the message receiver.
4.  After the data and signature are received, the receiver uses the public key to verify the signature.

Digital signatures are widely used to defend against data tampering and authenticate identities.

-   Case 1: You can use digital signatures to protect the integrity of your binary code and verify that the code is not manipulated. This helps provide a trusted execution environment.
-   Case 2: Digital signatures can also be used in digital certificate systems. In such a system, a CA provides a signature for digital certificates to certify the entity information, public and private key information, key purpose, expiration date, and issuer. The private key holder of a certificate uses the private key to sign a message. The message receiver uses the public key contained in the certificate to verify the message signature and uses the public key of the certificate issuer to verify the certificate.

For more information, see [Generate and verify a digital signature by using an asymmetric CMK](/intl.en-US/Key Service/Key type/Use asymmetric keys/Generate and verify a digital signature by using an asymmetric CMK.md).

## Key versions

KMS does not support automatic rotation of asymmetric CMKs due to the limits of public and private keys. You can call the [CreateKeyVersion](/intl.en-US/API Reference/Key/CreateKeyVersion.md) operation to create a key version in a specific CMK and generate a new pair of public and private keys. If you use a new key version to generate a digital signature or encrypt data, you must also distribute the new version of the public key.

In addition, unlike symmetric CMKs, asymmetric CMKs do not have a primary key version. Therefore, you must specify the corresponding CMK ID or CMK alias and a key version if you need to call the operations related to asymmetric CMKs in KMS.

## Public key operations

In most cases, you can call the [GetPublicKey](/intl.en-US/API Reference/Key/GetPublicKey.md) operation to obtain a public key and distribute it to users for encryption or verification. Then, the users can use cryptographic libraries such as OpenSSL and Java Cryptography Extension \(JCE\) to perform calculation in their business systems.

You can also call the [AsymmetricEncrypt](/intl.en-US/API Reference/Key/AsymmetricEncrypt.md) or [AsymmetricVerify](/intl.en-US/API Reference/Key/AsymmetricVerify.md) operation to perform public key operations. KMS records the logs of the calls and allows you to use Resource Access Management \(RAM\) to limit the use of public keys. Compared with calculation in business systems, KMS offers flexible features that better suit your needs.

## Private key operations

You can call only the [AsymmetricDecrypt](/intl.en-US/API Reference/Key/AsymmetricDecrypt.md) or [AsymmetricSign](/intl.en-US/API Reference/Key/AsymmetricSign.md) operation to use a private key to decrypt data or generate a digital signature.

