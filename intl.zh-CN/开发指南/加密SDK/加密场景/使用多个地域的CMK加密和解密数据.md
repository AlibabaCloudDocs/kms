# 使用多个地域的CMK加密和解密数据

阿里云在全球几十个地域，提供了密钥管理KMS、云数据库RDS和对象存储OSS等服务，这些服务在各个地域之间互相独立。使用加密SDK，您可以配置多个地域的KMS用户主密钥（CMK）来加密数据，构建跨地域的数据加密解密能力。

## 使用场景

在下列情形中，您可以通过加密SDK配置对应地域的KMS CMK，完成对敏感数据（例如：数据库列或字段、OSS对象等）的加密，使得加密数据具有对等地域的解密能力。

-   您使用了云数据库RDS的跨地域备份、同步等功能。
-   您使用了对象存储OSS的跨地域复制功能。
-   您通过其他方式对加密数据进行跨地域的复制。

## 加密数据

**加密机制**

![加密机制](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9791216061/p184561.png)

1.  调用KMS北京地域的[GenerateDataKey](/intl.zh-CN/API参考/密钥/GenerateDataKey.md)接口，得到数据密钥和数据密钥密文。
2.  调用KMS杭州地域的[Encrypt](/intl.zh-CN/API参考/密钥/Encrypt.md)接口，对数据密钥进行加密，得到数据密钥密文。
3.  根据加密算法及工作模式所需生成初始向量，使用数据密钥对您的数据进行加密，得到数据密文及认证信息。

    **说明：** 仅GCM（Galois Counter Mode）模式有认证信息。

4.  将两个数据密钥密文、加密上下文、算法信息封装到消息头，生成消息头的认证信息。
5.  将初始向量、数据密文、认证信息（可选）封装到消息体。
6.  将消息头和消息体封装为加密消息。

**加密代码示例**

本示例使用了华北2（cn-beijing）和华东1（cn-hangzhou）两个地域，您需要在两个地域创建AES或SM4类型的CMK，并且获取其阿里云资源名称（ARN），配置到以下代码中。其中华北2（cn-beijing）为主地域，在该地域调用KMS的GenerateDataKey接口产生数据密钥，使用华东1（cn-hangzhou）的CMK加密数据密钥。代码示例如下：

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
        //创建访问阿里云配置。
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        //创建SDK，传入访问阿里云配置。
        AliyunCrypto aliyunSDK = new AliyunCrypto(config);

        //创建provider，用于提供数据密钥或签名。
        BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_BEIJING_ARN);
        //设置不同的算法（可设置，默认为AES_GCM_NOPADDING_256）
        //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);
        // *** 设置多CMK（可设置，默认为单CMK）****
        provider.setMultiCmkId(CMK_ARN_LIST);

        //加密上下文。
        Map<String, String> encryptionContext = new HashMap<>();
        encryptionContext.put("one", "one");
        encryptionContext.put("two", "two");

        //调用加密接口。
        CryptoResult<byte[]> cipherResult = aliyunSDK.encrypt(provider, PLAIN_TEXT, encryptionContext);
        
        Assert.assertArrayEquals(PLAIN_TEXT, plainResult.getResult());
    }
}
```

**说明：** 本示例的完整代码请参见[MultiCmkSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/multi/MultiCmkSample.java)。

## 解密数据

**解密机制**

![解密机制](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9791216061/p184568.png)

1.  根据指定的CMK ARN，从加密消息的消息头中查找匹配的数据密钥密文。
2.  调用KMS的[Decrypt](/intl.zh-CN/API参考/密钥/Decrypt.md)接口，得到数据密钥。
3.  根据数据密钥，计算消息头的认证信息，对消息头中的认证信息进行比对并处理异常情况。
4.  根据加密算法及工作模式，对数据密文进行解密，得到数据。

**解密代码示例**

```
public class MultiCMKDecryptionExample {
    private static final String ACCESS_KEY_ID = "<AccessKeyId>";
    private static final String ACCESS_KEY_SECRET = "<AccessKeySecret>";
    
    private static final String CIPHER_TEXT_BASE64 = "==base64 encode of ciphertext==";

    private static final String CMK_BEIJING_ARN = "acs:kms:cn-beijing:UserId:key/CmkId";
    private static final String CMK_HANGZHOU_ARN = "acs:kms:cn-hangzhou:UserId:key/CmkId";

    
    public static void main(String[] args) {
        //创建访问阿里云配置。
        AliyunConfig config = new AliyunConfig();
        config.withAccessKey(ACCESS_KEY_ID, ACCESS_KEY_SECRET);

        //创建SDK，传入访问阿里云配置。
        AliyunCrypto aliyunSDK = new AliyunCrypto(config);

        //创建provider，用于提供数据密钥。
        // 北京地域进解密数据密钥密文时，指定北京地域的CMK ARN。
        BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_BEIJING_ARN);
        // 杭州地域进解密数据密钥密文时，指定杭州地域的CMK ARN。
        //BaseDataKeyProvider provider = new DefaultDataKeyProvider(CMK_HANGZHOU_ARN);
        //设置不同的算法（可设置，默认为AES_GCM_NOPADDING_256）
        //provider.setAlgorithm(CryptoAlgorithm.SM4_GCM_NOPADDING_128);

        //调用解密接口。
        byte[] cipherTextBytes = Base64.decode(CIPHER_TEXT_BASE64);
        CryptoResult<byte[]> plainResult = aliyunSDK.decrypt(provider, cipherTextBytes);
    }
}
```

