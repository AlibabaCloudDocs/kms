# Use CMKs in multiple regions to encrypt and decrypt data

Alibaba Cloud provides services such as Key Management Service \(KMS\), ApsaraDB RDS, and Object Storage Service \(OSS\) in dozens of regions around the world. The services in different regions are independent of each other. Encryption SDK allows you to use customer master keys \(CMKs\) managed by KMS in different regions to encrypt data in a single encryption process. This way, you can decrypt the data across regions.

## Scenario

In the following scenarios, you can use the cross-region encryption/decryption feature of Encryption SDK to encrypt and decrypt sensitive data, such as database fields and OSS objects:

-   The cross-region backup or synchronization feature of ApsaraDB RDS is used.
-   The cross-region replication feature of OSS is used.
-   Other cross-region replication methods are used.

## Encrypt data

**Encryption mechanism**

![Encryption mechanism](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4417018061/p201597.png)

1.  Call the [GenerateDataKey](/intl.en-US/API Reference/Key/GenerateDataKey.md) operation of KMS in the China \(Beijing\) region to generate a random data key. The plaintext and ciphertext of the data key are returned.
2.  Call the [Encrypt](/intl.en-US/API Reference/Key/Encrypt.md) operation of KMS in the China \(Hangzhou\) region to encrypt the data key. Another ciphertext of the data key is returned.
3.  Generate an initialization vector based on the encryption algorithm and working mode, and use the data key to encrypt your data. Ciphertext data and authentication information are returned.

    **Note:** Authentication information is available only when Galois/Counter Mode \(GCM\) is used.

4.  Encapsulate the two ciphertexts of the data key, the EncryptionContext strings used to encrypt the data key, and the related algorithm information into a message header, and generate authentication information for the message header.
5.  Encapsulate the initialization vector, ciphertext data, and authentication information into a message body. Authentication information is optional.
6.  Encapsulate the message header and message body into an encrypted message.

**Sample code for encryption**

In this example, the China \(Beijing\) and China \(Hangzhou\) regions are used. You must create AES or SM4 CMKs in both regions and obtain their ARNs, which are required in the code. China \(Beijing\) is used as the primary region. The GenerateDataKey operation is called in this region to generate a data key, and then the Encrypt operation is called in the China \(Hangzhou\) region to encrypt the data key. Sample code:

```
public class MultiCMKEncryptionExample {
    private static final String ACCESS_KEY_ID = "<AccessKeyId>";
    private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
    private static final String CMK_BEIJING_ARN = "acs:kms:cn-beijing:UserId:key/CmkId";
    private static final byte[] PLAIN_TEXT = "Hello World".getBytes(StandardCharsets.UTF_8);

    private static final String CMK_HANGZHOU_ARN = "acs:kms:cn-hangzhou:UserId:key/CmkId";

    private static final List<String> CMK_ARN_LIST;
    static {
        CMK_ARN_LIST = new ArrayList<>();
        CMK_ARN_LIST.add(CMK_HANGZHOU_ARN);
    }
    
    public static void main(String[] args) {
        // Configure Alibaba Cloud access parameters.
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        // Create an SDK and pass in the Alibaba Cloud access parameters.
        AliyunCrypto aliyunSDK = new AliyunCrypto(config);

        // Create a provider, which provides a data key or signature.
        BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_BEIJING_ARN);
        // Configure algorithms. If you do not specify this parameter, AES_GCM_NOPADDING_256 is used.
        //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);
        // *** Specify whether to use multiple CMKs. If you do not specify this parameter, a single CMK is used. ****
        provider.setMultiCmkId(CMK_ARN_LIST);

        // Configure EncryptionContext.
        Map<String, String> encryptionContext = new HashMap<>();
        encryptionContext.put("one", "one");
        encryptionContext.put("two", "two");

        // Call the Encrypt operation.
        CryptoResult<byte[]> cipherResult = aliyunSDK.encrypt(provider, PLAIN_TEXT, encryptionContext);
        
        Assert.assertArrayEquals(PLAIN_TEXT, plainResult.getResult());
    }
}
```

**Note:** For the complete sample code, see [MultiCmkSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/multi/MultiCmkSample.java).

## Decrypt data

**Decryption mechanism**

![Decryption mechanism](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/4417018061/p201598.png)

1.  Find the ciphertext data key that matches the specified CMK ARN from the header of the encrypted message.
2.  Call the [Decrypt](/intl.en-US/API Reference/Key/Decrypt.md) operation of KMS to obtain the plaintext of the data key.
3.  Calculate authentication information based on the data key, compare the calculation result with the authentication information in the message header, and handle exceptions.
4.  Decrypt the ciphertext data based on the encryption algorithm and working mode to obtain plaintext data.

**Sample code for decryption**

```
public class MultiCMKDecryptionExample {
    private static final String ACCESS_KEY_ID = "<AccessKeyId>";
    private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
    
    private static final String CIPHER_TEXT_BASE64 = "==base64 encode of ciphertext==";

    private static final String CMK_BEIJING_ARN = "acs:kms:cn-beijing:UserId:key/CmkId";
    private static final String CMK_HANGZHOU_ARN = "acs:kms:cn-hangzhou:UserId:key/CmkId";

    
    public static void main(String[] args) {
        // Configure Alibaba Cloud access parameters.
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        // Create an SDK and pass in the Alibaba Cloud access parameters.
        AliyunCrypto aliyunSDK = new AliyunCrypto(config);

        // Create a provider, which provides a data key.
        // If you want to decrypt the ciphertext data key in the China (Beijing) region, specify the ARN of the CMK in this region.
        BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_BEIJING_ARN);
        // If you want to decrypt the ciphertext data key in the China (Hangzhou) region, specify the ARN of the CMK in this region.
        //BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_HANGZHOU_ARN);
        // Configure algorithms. If you do not specify this parameter, AES_GCM_NOPADDING_256 is used.
        //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);

        // Call the Decrypt operation.
        byte[] cipherTextBytes = Base64.decode(CIPHER_TEXT_BASE64);
        CryptoResult<byte[]> plainResult = aliyunSDK.decrypt(provider, cipherTextBytes);
    }
}
```

