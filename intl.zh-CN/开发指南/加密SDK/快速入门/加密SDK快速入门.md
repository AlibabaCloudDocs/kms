# 加密SDK快速入门

加密SDK（Encryption SDK）是一个客户端密码库，通过与密钥管理服务KMS（Key Management Service）结合使用，帮助您快速实现数据的加解密、签名验签功能。本文以数据加解密为例，为您介绍如何快速使用加密SDK。

您可以访问[alibabacloud-encryption-sdk-java](https://github.com/aliyun/alibabacloud-encryption-sdk-java)，查看代码示例。

## 在本地安装加密SDK

1.  编译安装加密SDK。

    ```
    $ git clone https://github.com/aliyun/alibabacloud-encryption-sdk-java.git
    $ cd alibabacloud-encryption-sdk-java
    $ mvn clean install -DskipTests
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

本示例的完整代码请参见[SimpleEncryptAndDecryptSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/SimpleEncryptAndDecryptSample.java)。

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

