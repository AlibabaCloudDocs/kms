# Quick start of Encryption SDK for Java

Encryption SDK is a client-side encryption library. It is used with Key Management Service \(KMS\) to allow you to encrypt and decrypt data, as well as generate and verify signatures. This topic shows you how to use Encryption SDK for Java to encrypt and decrypt data.

For more information about the sample code, visit [alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java).

## Install Encryption SDK on your on-premises device

1.  Compile and install Encryption SDK.

    ```
    $ git clone https://github.com/aliyun/alibabacloud-encryption-sdk-java.git
    $ cd alibabacloud-encryption-sdk-java
    $ mvn clean install -DskipTests
    ```

2.  Add the dependency to your project.

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>alibabacloud-encryption-sdk-java</artifactId>
        <version>1.0.7</version>
    </dependency>
    ```


## Install Encryption SDK from the Maven repository

Add the alibabacloud-encryption-sdk-java dependency to your project. You project automatically downloads the published Java package of Encryption SDK from the Maven repository.

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>alibabacloud-encryption-sdk-java</artifactId>
    <version>1.0.x</version>
</dependency>
```

**Note:** The latest version of Encryption SDK is V1.0.7. For more information about the versions of Encryption SDK, visit [Alibabacloud Encryption SDK Java](https://mvnrepository.com/artifact/com.aliyun/alibabacloud-encryption-sdk-java).

## Sample code for data encryption and decryption

-   Encrypt and decrypt data of the byte array type.

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
    
            //2. Create an SDK object and pass in the Alibaba Cloud access parameters.
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //3. Create a provider that provides the data key or signature.
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
            // Configure the algorithm. The default algorithm is AES_GCM_NOPADDING_256.
            //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);
    
            //4. Configure the encryption context.
            Map<String, String> encryptionContext = new HashMap<>();
            encryptionContext.put("one", "one");
            encryptionContext.put("two", "two");
    
            //5. Call the encrypt and decrypt methods.
            CryptoResult<byte[]> cipherResult = aliyunSDK.encrypt(provider, PLAIN_TEXT, encryptionContext);
            CryptoResult<byte[]> plainResult = aliyunSDK.decrypt(provider, cipherResult.getResult());
    
            Assert.assertArrayEquals(PLAIN_TEXT, plainResult.getResult());
        }
    }
    ```

    For more information about the complete sample code, visit [SimpleEncryptAndDecryptSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/SimpleEncryptAndDecryptSample.java).

-   Encrypt and decrypt data of the byte stream type.

    ```
    public class FileStreamSample {
        private static final String FILE = "README.md";
        // accessKeyId accessKeySecret
        private static final String ACCESS_KEY_ID = "<AccessKeyId>";
        private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
        // The log system.
        private static final Logger LOGGER = LoggerFactory.getLogger(FileStreamSample.class);
        // The ID of the customer master key (CMK) in the Alibaba Cloud Resource Name (ARN) format.
        private static final String CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
    
        public static void main(String[] args) throws IOException {
            AliyunConfig config = new AliyunConfig();
            config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);
            encryptStream(config);
            decryptStream(config);
            Assert.assertEquals(getFileMD5(FILE), getFileMD5(FILE + ".decrypted"));
        }
    
        private static void encryptStream(AliyunConfig config) throws IOException {
            //1. Create an SDK object and pass in the Alibaba Cloud access parameters.
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //2. Configure the encryption context.
            final Map<String, String> encryptionContext = new HashMap<>();
            encryptionContext.put("this", "context");
            encryptionContext.put("can help you", "to confirm");
            encryptionContext.put("this data", "is your original data");
    
            //3. Create a provider that provides the data key.
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
    
            //4. Create input and output streams.
            FileInputStream inputStream = new FileInputStream(FILE);
            FileOutputStream outputStream = new FileOutputStream(FILE + ".encrypted");
    
            //5. Call the encrypt method.
            try {
                aliyunSDK.encrypt(provider, inputStream, outputStream, encryptionContext);
            } catch (InvalidAlgorithmException e) {
                System.out.println("Failed.") ;
                System.out.println("Error message: " + e.getMessage());
            }
        }
    
        private static void decryptStream(AliyunConfig config) throws IOException {
            //1. Create an SDK object and pass in the Alibaba Cloud access parameters.
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //2. Create a provider that provides the data key.
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
    
            //3. Create input and output streams.
            FileInputStream inputStream = new FileInputStream(FILE + ".encrypted");
            FileOutputStream outputStream = new FileOutputStream(FILE + ".decrypted");
    
            //4. Call the decrypt method.
            try {
                aliyunSDK.decrypt(provider, inputStream, outputStream);
            } catch (InvalidAlgorithmException e) {
                System.out.println("Failed.") ;
                System.out.println("Error message: " + e.getMessage());
            }
        }
    
        private static String getFileMD5(String fileName) {
            File file = new File(fileName);
            if  (! file.isFile()) {
                return null;
            }
            MessageDigest digest;
            byte[] buffer = new byte[4096];
            try (FileInputStream in = new FileInputStream(file)){
                digest = MessageDigest.getInstance("MD5");
                int len;
                while  ((len = in.read(buffer)) ! = -1) {
                    digest.update(buffer,  0 , len);
                }
                return Hex.encodeHexString(digest.digest());
            }  catch  (Exception e) {
                e.printStackTrace();
            }
            return null;
        }
    }
    ```


