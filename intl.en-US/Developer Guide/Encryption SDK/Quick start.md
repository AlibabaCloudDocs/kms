# Quick start

Encryption SDK is a client-side encryption library. It is used with Key Management Service \(KMS\) to allow you to easily encrypt and decrypt data, as well as generate and verify signatures. This topic describes how to use Encryption SDK to encrypt and decrypt data.

You can view the sample code at [alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java).

## Install Encryption SDK on your on-premises machine

1.  Compile and install Encryption SDK.

    ```
    $ git clone https://github.com/aliyun/alibabacloud-encryption-sdk-java.git
    $ cd alibabacloud-encryption-sdk-java
    $ mvn clean install -DskipTests
    ```

2.  Add dependencies to the related project.

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>alibabacloud-encryption-sdk-java</artifactId>
        <version>1.0.7</version>
    </dependency>
    ```


## Install Encryption SDK based on a Maven repository

Add the alibabacloud-encryption-sdk-java dependency to the project. This way, the published Java package can be automatically downloaded from the Maven repository.

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>alibabacloud-encryption-sdk-java</artifactId>
    <version>1.0.x</version>
</dependency>
```

**Note:** The latest version of Encryption SDK is 1.0.7. For more information about the versions of Encryption SDK, see [Alibaba Cloud Encryption SDK for Java](https://mvnrepository.com/artifact/com.aliyun/alibabacloud-encryption-sdk-java).

## Sample code for data encryption and decryption

For the complete code, see [SimpleEncryptAndDecryptSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/SimpleEncryptAndDecryptSample.java).

```
public class BasicEncryptionExample {
    private static final String ACCESS_KEY_ID = "<AccessKeyId>";
    private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
    private static final String CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
    private static final byte[] PLAIN_TEXT = "Hello World".getBytes(StandardCharsets.UTF_8);

    public static void main(String[] args) {
        //1. Configure Alibaba Cloud access parameters.
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        //2. Create an SDK and pass in the Alibaba Cloud access parameters.
        AliyunCrypto aliyunSDK = new AliyunCrypto(config);

        //3. Create a provider that provides a data key or signature.
        BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
        //Configure algorithms. If you do not specify this parameter, AES_GCM_NOPADDING_256 is used.
        //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);

        //4. Configure EncryptionContext.
        Map<String, String> encryptionContext = new HashMap<>();
        encryptionContext.put("one", "one");
        encryptionContext.put("two", "two");

        //5. Call the Encrypt and Decrypt operations.
        CryptoResult<byte[]> cipherResult = aliyunSDK.encrypt(provider, PLAIN_TEXT, encryptionContext);
        CryptoResult<byte[]> plainResult = aliyunSDK.decrypt(provider, cipherResult.getResult());

        Assert.assertArrayEquals(PLAIN_TEXT, plainResult.getResult());
    }
}
```

