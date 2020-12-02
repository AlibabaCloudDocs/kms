# 从ECS实例安全访问KMS

您可以为云服务器ECS创建RAM服务角色，使ECS实例内的应用程序可以通过STS角色扮演的方式访问KMS，然后使用加密SDK实现数据加解密。

1.  为ECS创建RAM服务角色并授权，使其可以访问KMS。

    具体操作，请参见[使用实例RAM角色访问其他云产品](/cn.zh-CN/最佳实践/使用实例RAM角色访问其他云产品.md)。

    在步骤一中，您需要为RAM角色授权管理KMS的权限策略，内容如下：

    ```
    {
        "Statement": [
            {
                "Action": [
                    "kms:*", 
                ], 
                "Effect": "Allow", 
                "Resource": "*"
            }
        ], 
        "Version": "1"
    }
    ```

2.  使用加密SDK实现数据加解密。

    ```
    package com.aliyun.encryptionsdk.examples.credentials;
    
    import com.aliyun.encryptionsdk.AliyunConfig;
    import com.aliyun.encryptionsdk.AliyunCrypto;
    import com.aliyun.encryptionsdk.exception.InvalidAlgorithmException;
    import com.aliyun.encryptionsdk.exception.UnFoundDataKeyException;
    import com.aliyun.encryptionsdk.model.CryptoResult;
    import com.aliyun.encryptionsdk.provider.dataKey.DefaultDataKeyProvider;
    
    import java.util.Collections;
    
    import static org.junit.Assert.assertArrayEquals;
    
    /**
     *
     * 通过ECS实例RAM角色进行访问认证。
     */
    public class EcsRamRoleSample {
        private static final String PLAIN_TEXT = "this is test.";
        private static final String cmkArn = "acs:kms:RegionId:UserId:key/CmkId";
        private static final String ecRamRoleName = "EcsRamRoleTest";
        public static void main(String[] args) {
            AliyunConfig config = new AliyunConfig();
            //设置RAM角色。
            config.withEcsRamRole(ecRamRoleName);
            
            AliyunCrypto crypto = new AliyunCrypto(config);
            
            DefaultDataKeyProvider defaultDataKeyProvider = new DefaultDataKeyProvider(cmkArn);
            try {
                CryptoResult<byte[]> encryptResult = crypto.encrypt(defaultDataKeyProvider, PLAIN_TEXT.getBytes(), Collections.singletonMap("sample", "Context"));
                CryptoResult<byte[]> decryptResult = crypto.decrypt(defaultDataKeyProvider, encryptResult.getResult());
                assertArrayEquals(decryptResult.getResult(), PLAIN_TEXT.getBytes());
            } catch (InvalidAlgorithmException | UnFoundDataKeyException e) {
                System.out.println("Failed.");
                System.out.println("Error message: " + e.getMessage());
            }
        }
    }
    ```

    **说明：** 完整代码示例请参见[EcsRamRoleSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/credentials/EcsRamRoleSample.java)。


