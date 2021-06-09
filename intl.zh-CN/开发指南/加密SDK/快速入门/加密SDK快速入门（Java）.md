# 加密SDK快速入门（Java）

加密SDK（Encryption SDK）是一个客户端密码库，通过与密钥管理服务KMS（Key Management Service）结合使用，帮助您快速实现数据的加解密、签名验签功能。本文以Java语言为例，为您介绍如何快速使用加密SDK进行数据加解密。

您可以访问[alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java)，查看代码示例。

## 在本地安装加密SDK

1.  编译安装加密SDK。

    ```
    git clone https://github.com/aliyun/alibabacloud-encryption-sdk-java.git
    cd alibabacloud-encryption-sdk-java
    mvn clean install -DskipTests
    ```

2.  在项目中添加依赖。

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>alibabacloud-encryption-sdk-java</artifactId>
        <version>1.0.7</version>
    </dependency>
    ```


## 通过Maven仓库安装加密SDK

在项目中添加alibabacloud-encryption-sdk-java的依赖，可从Maven仓库中自动下载发布的Java安装包。

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>alibabacloud-encryption-sdk-java</artifactId>
    <version>1.0.x</version>
</dependency>
```

**说明：** 加密SDK当前版本为1.0.7。具体版本，请参见[Alibabacloud Encryption SDK Java](https://mvnrepository.com/artifact/com.aliyun/alibabacloud-encryption-sdk-java)。

## 数据加解密示例

-   对字节数组类型的数据进行加解密

    ```
    public class BasicEncryptionExample {
        private static final String ACCESS_KEY_ID = "<AccessKeyId>";
        private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
        private static final String CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
        private static final byte[] PLAIN_TEXT = "Hello World".getBytes(StandardCharsets.UTF_8);
    
        public static void main(String[] args) {
            //1.创建访问aliyun配置。
            AliyunConfig config = new AliyunConfig();
            config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);
    
            //2.创建SDK，传入访问aliyun配置。
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //3.创建provider，用于提供数据密钥或签名。
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
            //设置不同的算法（默认为AES_GCM_NOPADDING_256）。
            //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);
    
            //4.加密上下文。
            Map<String, String> encryptionContext = new HashMap<>();
            encryptionContext.put("one", "one");
            encryptionContext.put("two", "two");
    
            //5.调用加密和解密接口。
            CryptoResult<byte[]> cipherResult = aliyunSDK.encrypt(provider, PLAIN_TEXT, encryptionContext);
            CryptoResult<byte[]> plainResult = aliyunSDK.decrypt(provider, cipherResult.getResult());
    
            Assert.assertArrayEquals(PLAIN_TEXT, plainResult.getResult());
        }
    }
    ```

    本示例的完整代码请参见[SimpleEncryptAndDecryptSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/SimpleEncryptAndDecryptSample.java)。

-   对字节流类型的数据进行加解密

    ```
    public class FileStreamSample {
        private static final String FILE = "README.md";
        // accessKeyId accessKeySecret
        private static final String ACCESS_KEY_ID = "<AccessKeyId>";
        private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
        // 日志系统。
        private static final Logger LOGGER = LoggerFactory.getLogger(FileStreamSample.class);
        // ARN格式的用户主密钥ID。
        private static final String CMK_ARN = "acs:kms:RegionId:UserId:key/CmkId";
    
        public static void main(String[] args) throws IOException {
            AliyunConfig config = new AliyunConfig();
            config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);
            encryptStream(config);
            decryptStream(config);
            Assert.assertEquals(getFileMD5(FILE), getFileMD5(FILE + ".decrypted"));
        }
    
        private static void encryptStream(AliyunConfig config) throws IOException {
            //1.创建SDK，传入访问aliyun配置。
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //2.构建加密上下文。
            final Map<String, String> encryptionContext = new HashMap<>();
            encryptionContext.put("this", "context");
            encryptionContext.put("can help you", "to confirm");
            encryptionContext.put("this data", "is your original data");
    
            //3.创建提供数据密钥的provider。
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
    
            //4.创建输入输出流。
            FileInputStream inputStream = new FileInputStream(FILE);
            FileOutputStream outputStream = new FileOutputStream(FILE + ".encrypted");
    
            //5.调用加密接口。
            try {
                aliyunSDK.encrypt(provider, inputStream, outputStream, encryptionContext);
            } catch (InvalidAlgorithmException e) {
                System.out.println("Failed.");
                System.out.println("Error message: " + e.getMessage());
            }
        }
    
        private static void decryptStream(AliyunConfig config) throws IOException {
            //1.创建SDK，传入访问aliyun配置。
            AliyunCrypto aliyunSDK = new AliyunCrypto(config);
    
            //2.创建提供数据密钥的provider。
            BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_ARN);
    
            //3.创建输入输出流。
            FileInputStream inputStream = new FileInputStream(FILE + ".encrypted");
            FileOutputStream outputStream = new FileOutputStream(FILE + ".decrypted");
    
            //4.调用解密接口。
            try {
                aliyunSDK.decrypt(provider, inputStream, outputStream);
            } catch (InvalidAlgorithmException e) {
                System.out.println("Failed.");
                System.out.println("Error message: " + e.getMessage());
            }
        }
    
        private static String getFileMD5(String fileName) {
            File file = new File(fileName);
            if  (!file.isFile()) {
                return null;
            }
            MessageDigest digest;
            byte[] buffer = new byte[4096];
            try (FileInputStream in = new FileInputStream(file)){
                digest = MessageDigest.getInstance("MD5");
                int len;
                while  ((len = in.read(buffer)) != -1) {
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


