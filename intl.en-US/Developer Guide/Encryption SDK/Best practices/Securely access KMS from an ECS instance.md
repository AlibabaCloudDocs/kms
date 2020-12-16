# Securely access KMS from an ECS instance

You can create a RAM role for ECS and assume the RAM role to obtain a Security Token Service \(STS\) token. Then, you can use the token to access KMS from an ECS instance and use Encryption SDK to encrypt and decrypt the related data.

1.  Create a RAM role for ECS and authorize it to access KMS.

    For more information, see [Use RAM roles to access other Alibaba Cloud services](/intl.en-US/Best Practices/Use RAM roles to access other Alibaba Cloud services.md).

    In this step, you must create a policy that grants management permissions on KMS and attach the policy to the RAM role. The following example shows the policy:

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

2.  Use Encryption SDK to encrypt and decrypt data.

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
     * Use the RAM role for access authentication.
     */
    public class EcsRamRoleSample {
        private static final String PLAIN_TEXT = "this is test.";
        private static final String cmkArn = "acs:kms:RegionId:UserId:key/CmkId";
        private static final String ecRamRoleName = "EcsRamRoleTest";
        public static void main(String[] args) {
            AliyunConfig config = new AliyunConfig();
            // Configure the RAM role.
            config.withEcsRamRole(ecRamRoleName);
            
            AliyunCrypto crypto = new AliyunCrypto(config);
            
            DefaultDataKeyProvider defaultDataKeyProvider = new DefaultDataKeyProvider(cmkArn);
            try {
                CryptoResult<byte[]> encryptResult = crypto.encrypt(defaultDataKeyProvider, PLAIN_TEXT.getBytes(), Collections.singletonMap("sample", "Context"));
                CryptoResult<byte[]> decryptResult = crypto.decrypt(defaultDataKeyProvider, encryptResult.getResult());
                assertArrayEquals(decryptResult.getResult(), PLAIN_TEXT.getBytes());
            } catch (InvalidAlgorithmException | UnFoundDataKeyException e) {
                System.out.println("Failed.") ;
                System.out.println("Error message: " + e.getMessage());
            }
        }
    }
    ```

    **Note:** For the complete sample code, see [EcsRamRoleSample.java](https://github.com/aliyun/alibabacloud-encryption-sdk-java/blob/master/src/examples/java/com/aliyun/encryptionsdk/examples/credentials/EcsRamRoleSample.java).


