# Overview

Certificates Manager provides a highly available and secure system for managing keys and certificates. Certificates Manager also allows you to use certificates to generate and verify signatures.

## Architecture

Applications that require certificates can use Certificates Manager to generate certificate signing requests \(CSRs\) and import or export digital certificates and their certificate chains. Certificates Manager use hardware security modules \(HSMs\) to protect the security of digital keys and certificates.

![Arcitecture](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/3989679161/p270295.png)

## Benefits

-   Secure key storage

    Certificates Manager uses HSMs to ensure that keys and certificates are securely generated and stored. For more information, see [Overview](/intl.en-US/Key Service/Managed HSM/Overview.md).

-   Lifecycle management

    Certificates Manager allows you to manage keys and certificates. You can generate CSRs, import certificates and certificate chains, verify the signatures of certificate chains, and check the certificate validity.

-   Diverse public key algorithms

    Certificates Manager supports multiple public key algorithms such as Rivest–Shamir–Adleman \(RSA\) 2048, elliptic curve \(EC\) P256, and EC SM2. Certificates Manager supports the X.509 v3 certificate format and complies with the relevant public key infrastructure \(PKI\) and certificate authority \(CA\) standards.

-   Easy API integration

    Certificates Manager provides multiple API operations to help you efficiently integrate the certificate service with your development environment. Certificates Manager accelerates product deployment and allows you to efficiently roll out certificate-related features.


