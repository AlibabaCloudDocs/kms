# Encrypt sensitive data in a database

Encryption is a proactive measure to protect data in a database. Encryption prevents data leaks that are caused by plaintext storage and data theft by privileged users. Encryption also helps defend against hackers that break through the security boundary. This way, the issue of sensitive data leaks can be fundamentally resolved. The data encrypted on the client side by the encryption SDK can be stored in a relational database or a non-relational database. This topic describes the scenarios of sensitive data encryption in a database and how to encrypt and decrypt data. This topic also provides an example on how to encrypt sensitive data in a database.

## Scenarios

-   Prevent sensitive data leaks caused by plaintext storage after a data breach.

    In most cases, data in a database is stored and used in plaintext. If data files or backup files are disclosed, serious data leaks may occur. In data breach attacks, data stored in plaintext has no secrets for attackers. To resolve this issue, you must encrypt your data to prevent data leaks.

-   Prevent data leaks caused by data theft by privileged users.

    Database encryption is independent of the permission control system of a database. Database encryption can help enhance permission control. You can use a dedicated encryption system to configure access permissions on sensitive data. This ensures data security by effectively controlling the access to sensitive data from privileged users such as database superusers.


## How to encrypt and decrypt data

-   Encryption
    1.  Create a data key.

        Encryption SDK calls the GenerateDataKey operation to request a data key from Key Management Service \(KMS\). KMS returns the data key and its ciphertext.

    2.  Encrypt and store data.
        1.  Use the data key to encrypt data and encode the ciphertext data by using the Base64 algorithm.
        2.  Store the Base64-encoded ciphertext data in a database.
-   Decryption

    Query and decrypt data.

    1.  Read ciphertext data from the database.
    2.  Decode the ciphertext data by using the Base64 algorithm. Encryption SDK calls the Decrypt operation of KMS to decrypt the ciphertext data key. KMS returns the decrypted data key to Encryption SDK.
    3.  Decrypt data. Encryption SDK uses the data key to decrypt the ciphertext data and obtain the plaintext data.

## Example

Encryption SDK encrypts data to be transmitted from applications to databases. KMS generates and manages the encryption keys.

The following code provides examples on how to encrypt and decrypt the email field in the User table by using Spring Data JPA and Python. In these examples, each field uses a data key. Data keys are cached during decryption. When you query the same field for multiple times, you can use the data key that is cached.

To ensure that a field can store encrypted data, you must increase the size of the field to three times that of the original size.



For more information about the examples of sensitive data encryption in databases, visit [alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/tree/master/src/examples/java/com/aliyun/encryptionsdk/examples/jpaencryption) and [alibabacloud-encryption-sdk-python](https://github.com/aliyun/alibabacloud-encryption-sdk-python/blob/master/examples/src/rds/rds_sample.py).

