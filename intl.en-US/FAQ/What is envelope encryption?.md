# What is envelope encryption?

Envelope encryption is an encryption mechanism similar to digital envelope technology. The technology allows you to store, transfer and use encrypted data by encapsulating their data keys \(DKs\) in an envelope, instead of encrypting/decrypting data directly with Customer Master Keys \(CMKs\).

## Direct encryption/decryption services are not suitable for cloud scenarios.

Using cloud services to directly encrypt/decrypt user data creates the following problems:

-   Security risks
    -   When a client transmits sensitive information over the Internet to a service, there are many risks, including eavesdropping and phishing.
-   Difficulty proving trust and credibility
    -   Users may not trust some cloud services, so they may not be willing to upload sensitive data.
    -   It is difficult for cloud services to prove that they will not misuse or leak data.
-   Poor performance, high costs
    -   Large volumes of data must be transmitted to servers through secure channels and then encrypted before being returned to users. This has a major impact on users' service performance.
    -   We all know that, in a distributed system, we should do our best to implement mobile computing instead of mobile data, as large volumes of mobile data will lead to extremely high costs.

## Envelope encryption scenarios: Encrypt a local file

|Legend|Definition|
|:-----|:---------|
|![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821713525_en-US.png)|Customer Master Key|
|![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821713526_en-US.png)|Plaintext data key|
|![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821713527_en-US.png)|Ciphertext data key|
|![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821813528_en-US.png)|Plaintext file|
|![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821813529_en-US.png)|Ciphertext file|

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821813530_en-US.png)

## Encryption process

1.  Create a CMK.
2.  Call the [t22707.md\#](/intl.en-US/API Reference/Key/GenerateDataKey.md) interface of the KMS to generate a data key. You can obtain a plaintext data key and a ciphertext data key.
3.  Use the plaintext data key to encrypt the file and generate a ciphertext file.
4.  Save the ciphertext data key and the ciphertext file to a persistent storage device or service.

![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/22684/154018821813531_en-US.png)

## Decryption process

1.  Read the ciphertext data key and the ciphertext file from the persistent storage device or service.
2.  Call the [t22699.md\#](/intl.en-US/API Reference/Key/Decrypt.md) interface of the KMS to decrypt the ciphertext data key to obtain the plaintext data key.
3.  Use the plaintext data key to decrypt the file.

