# Overview

Encryption SDK is a client-side encryption library. It is used with Key Management Service \(KMS\) to allow you to encrypt and decrypt data, as well as generate and verify signatures.

## Features

-   Encryption SDK is integrated with KMS to manage and protect keys. This meets security and compliance requirements.
-   Encryption SDK provides simple cryptographic operations. For example, Encryption SDK allows you to use a unique key in each session to encrypt messages. You can also use Encryption SDK to generate and verify signatures.
-   Encryption SDK adopts an extensible design pattern that supports custom cryptographic operations. For example, you can customize Encryption SDK to use the same data key in multiple sessions.

## Benefits

-   Encryption SDK encapsulates best practices to simplify coding.

    Encryption SDK creates a unique data key for each piece of data that you want to encrypt. This way, each encryption session uses a unique data key. This follows best practices for cryptography design.

-   Encryption SDK has high business compatibility.

    Encryption SDK supports various encryption algorithms, working modes, and padding methods to meet different business and migration requirements.

-   Encryption SDK supports cross-region data encryption and decryption.

    Encryption SDK allows you to configure different customer master keys \(CMKs\) in different regions. You can encrypt data by using a single line of code and decrypt the data in different regions. This ensures cross-region data availability and disaster recovery.


## Quick start

For more information about the quick start of Encryption SDK for different programming languages, see the following topics:

-   [Quick start of Encryption SDK for Java](/intl.en-US/Developer Guide/Encryption SDK/Quick Start/Quick start of Encryption SDK for Java.md)
-   [t2038837.md\#]()

