# Data formats

This topic describes the formats of data in the data encryption and signing output of Encryption SDK to help you better understand the encryption and signing information.

## Data encryption

-   Data encryption output

    |Data encryption output|Component|Description|
    |----------------------|---------|-----------|
    |Message header|Version|The current version is 1.|
    |Algorithms|For more information, see [Algorithms](#table_u66_m34_mts). |
    |Data key list|At least one data key is displayed. The information of each data key consists of the following parts:

    -   The Alibaba Cloud Resource Name \(ARN\) of the customer master key \(CMK\) that is used to encrypt the data key. An ARN includes a region ID, user ID, and CMK ID, and is presented in the format of `acs:kms:RegionId:UserId:key/CmkId`.
    -   The ciphertext of the data key encrypted by using the primary version of the specified CMK. The ciphertext is the value of the CipherBlob parameter that is returned for the [GenerateDataKey](/intl.en-US/API Reference/Key/GenerateDataKey.md) operation. |
    |EncryptionContext|EncryptionContext is used as additional authentication data for symmetric encryption algorithms.|
    |Initialization vector for header authentication|The initialization vector that is used to calculate header authentication information. The value is a random number.|
    |Header authentication information|The system calculates the header authentication information based on Galois Message Authentication Code \(GMAC\). If verification fails, an error is returned, indicating that the format of the encryption message is invalid.|
    |Message body|Initialization vector|An initialization vector is an input value with a fixed length. In most cases, it is a random number or pseudo-random number.|
    |Ciphertext data|The ciphertext returned after data is encrypted.|
    |Authentication data|The authentication data returned when Galois/Counter Mode \(GCM\) is used. Authentication data is used to verify data integrity. If the verification fails, a decryption failure is reported.|

    The following table describes the formats of algorithm information in a message header.

    |No.|Algorithm information|Algorithm|Working mode|Length of key \(bit\)|Length of initialization vector \(byte\)|
    |---|---------------------|---------|------------|---------------------|----------------------------------------|
    |1|AES\_GCM\_NOPADDING\_128|AES|GCM|128|12|
    |2|AES\_GCM\_NOPADDING\_256|AES|GCM|256|12|
    |3|AES\_CBC\_NOPADDING\_128|AES|CBC|128|16|
    |4|AES\_CBC\_NOPADDING\_256|AES|CBC|256|16|
    |5|AES\_CBC\_PKCS5\_128|AES|CBC|128|16|
    |6|AES\_CBC\_PKCS5\_256|AES|CBC|256|16|
    |7|AES\_CTR\_NOPADDING\_128|AES|CTR|128|16|
    |8|AES\_CTR\_NOPADDING\_256|AES|CTR|256|16|
    |9|SM4\_GCM\_NOPADDING\_128|SM4|GCM|128|16|
    |10|SM4\_CBC\_NOPADDING\_128|SM4|CBC|128|16|
    |11|SM4\_CBC\_PKCS5\_128|SM4|CBC|128|16|
    |12|SM4\_CTR\_NOPADDING\_128|SM4|CTR|128|16|

    **Note:** Only AES\_GCM\_NOPADDING\_128 and AES\_GCM\_NOPADDING\_256 contain authentication data, which is 16 bytes in length.

-   Definition of the data formats

    Data encryption output is encoded in ASN.1. The following code provides the ASN.1 syntax for the output data:

    ```
    EncryptionMessage ::== SEQUENCE {
        encryptionHead        EncryptionHead           -- Message header
        encryptionBody        EncryptionBody           -- Message body
    }
    
    EncryptionHead ::== SEQUENCE {
        version               INTEGER                  -- Version
        algorithm             INTEGER                  -- Algorithm
        encryptedDataKeys     SET EncryptedDataKey     -- Data keys
        encryptionContext     SET EncryptionContext    -- EncryptionContext
        headerIv              OCTECT STRING            -- Initialization vector for header authentication
        headerAuthTag         OCTECT STRING            -- Header authentication information
    }
    
    EncryptionBody ::== SEQUENCE{
        iv                    OCTECT STRING            -- Initialization vector
        cipherText            OCTECT STRING            -- Ciphertext
        authTag               OCTECT STRING            -- GCM authentication information
    }
    
    EncryptedDataKey ::== SEQUENCE {
        cmkArn                OCTECT STRING            -- ARN of a KMS CMK
        encryptedDataKey      OCTECT STRING            -- Ciphertext of a data key
    }
    
    EncryptionContext ::== SEQUENCE {
        key                   OCTECT STRING
        value                 OCTECT STRING
    }
    ```

-   Example of data encryption output

    ```
    SEQUENCE (2 elem)
      SEQUENCE (6 elem)
        INTEGER 1                                                       // Version
        INTEGER 2                                                       // Algorithm
        SET (2 elem)                                                    // Data keys
          SEQUENCE (2 elem)
            OCTET STRING (77 byte) acs:kms:cn-beijing:1540355698xxxxx:key/2fad5f44-9573-4f28-8956-xxxx...
            OCTET STRING (108 byte) 36613739356232362D626163642xxxx262642D383630612D323563313839316131663...
          SEQUENCE (2 elem)
            OCTET STRING (77 byte) acs:kms:cn-hangzhou:1540355698xxxxx:key/f6d61352-82bb-450a-b105-xxxx...
            OCTET STRING (108 byte) 62623630646439352D343165302xxxx237382D616233332D356262636136643633643...
        SET (5 elem)                                                    // EncryptionContext set
          SEQUENCE (2 elem)
            OCTET STRING (11 byte) encryption
            OCTET STRING (7 byte) context
          SEQUENCE (2 elem)
            OCTET STRING (7 byte) is not
            OCTET STRING (6 byte) secret
          SEQUENCE (2 elem)
            OCTET STRING (9 byte) but adds
            OCTET STRING (15 byte) useful metadata
          SEQUENCE (2 elem)
            OCTET STRING (18 byte) that can help you
            OCTET STRING (17 byte) be confident that
          SEQUENCE (2 elem)
            OCTET STRING (26 byte) the data you are handling
            OCTET STRING (23 byte) is what you think it is
        OCTET STRING (12 byte) E66C1CE19C79F3FBCD62858D                  // Initialization vector for header authentication
        OCTET STRING (16 byte) CEEC46C65670E82CD78028AC0104D083          // Header authentication data
      SEQUENCE (3 elem)                                                  // Encrypted message
        OCTET STRING (12 byte) EF49E2CBB768A7AD0FB0FE20                  // Initialization vector
        OCTET STRING (13 byte) 89A4AB43CD793F7711767C491A                // Ciphertext data
        OCTET STRING (16 byte) 2E93DA019B7A6507155BA3AA252750E3          // Authentication data
    ```

-   Length of data encryption output
    -   \(108 bytes + 77 bytes\) × Number of CMKs

        **Note:** The ARN of a CMK is 108 bytes in length. The value of the CipherBlob parameter returned by the GenerateDataKey operation is 77 bytes in length.

    -   Length of EncryptionContext
    -   Length of ASN.1-encoded data: 30 bytes
    -   Length of ciphertext data
    -   Length of an initialization vector
    -   Length of authentication information

## Data signing

Encryption SDK uses the [AsymmetricSign](/intl.en-US/API Reference/Key/AsymmetricSign.md) operation of KMS to sign data. This operation returns a signature value in the binary format.

