# Overview

Encryption SDK is a client-side encryption library. It is used with Key Management Service \(KMS\) to allow you to easily encrypt and decrypt data, as well as generate and verify signatures.

## Features

-   Is integrated with KMS to protect keys and meet security and compliance requirements.
-   Provides simple API operations that encrypt each session \(message\) with an individual data key and generate and verify signatures.
-   Provides an extensible design pattern that supports custom cryptographic operations, such as to encrypt multiple sessions with the same data key.

## Benefits

-   Encapsulates best practices to simplify code development.

    Encryption SDK creates a unique data key for each piece of data that you want to encrypt. The "one session, one key" best practice is followed.

-   Has high business compatibility.

    Encryption SDK supports various encryption algorithms, working modes, and padding methods to meet different business and migration requirements.

-   Supports cross-region data encryption and decryption.

    Encryption SDK allows you to configure customer master keys \(CMKs\) in different regions in a single line of code to encrypt data. This way, you can decrypt the data in different regions, which ensures cross-region data availability and disaster recovery.


## Sample code

To view the sample code, see [alibabacloud-encryption-sdk-java-examples](https://github.com/aliyun/alibabacloud-encryption-sdk-java/tree/master/src/examples).

