# Java SDK示例

本文以Java语言为例，为您介绍如何使用KMS Java SDK。

## 背景信息

-   您可以访问 [开源代码仓库](https://github.com/aliyun/alibabacloud-kms-demo)，查看更多语言和场景的代码示例。同时也欢迎您提出宝贵意见，或者提供代码示例。
-   关于KMS API的详情，请参见[API概览](/cn.zh-CN/API参考/API概览.md)。

## 准备工作

1.  获取Java SDK的依赖声明，需要获取的版本请参见[SDK概览](/cn.zh-CN/SDK参考/SDK概览.md)。示例如下：

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.2</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-kms</artifactId>
        <version>2.10.1</version>
    </dependency>
    ```

2.  根据您使用的KMS地域，确认正确的KMS服务接入地址。详情请参见[服务地址](/cn.zh-CN/API参考/调用方式/请求结构.md)。

    **说明：** KMS支持通过公网或者VPC访问，在使用SDK时，需要指定不同的参数。

    -   如果仅指定地域的标识符，SDK会默认使用指定地域的KMS公网接入地址。
    -   如果需要访问KMS的VPC接入地址，需要手动为SDK指定接入地址参数。

## 示例：KmsSample

1.  创建一个KmsClient（调用封装类）。

    ```
    package com.aliyun.kms.samples;
    
    import java.util.*;
    
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.*;
    
    //Current KMS SDK version:2016-01-20
    import com.aliyuncs.kms.model.v20160120.*;
    import com.aliyuncs.kms.model.v20160120.ListKeysResponse.Key;
    import com.aliyuncs.profile.*;
    
    public class KmsClient
    {
        private DefaultAcsClient kmsClient;
    
        /**
         * 创建KmsClient，只需要指定regionId，SDK自动配置相应地域的公网Endpoint。
         */
        public static KmsClient getClientForPublicEndpoint(String regionId, String accessKeyId, String accessKeySecret) {
            /**
             * Construct an Aliyun Client:
             * Set RegionId, AccessKeyId and AccessKeySecret
             */
            IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            DefaultAcsClient client = new DefaultAcsClient(profile);
            return new KmsClient(client);
        }
    
        /**
         * 创建KmsClient，使用自定义Endpoint，通常用于访问VPC Endpoint。
         */
        public static KmsClient getClientForVpcEndpoint(String regionId, String accessKeyId, String accessKeySecret, String endpoint) {
            //添加自定义Endpoint
            DefaultProfile.addEndpoint(regionId, "kms", endpoint);
    
            IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
            HttpClientConfig clientConfig = HttpClientConfig.getDefault();
            profile.setHttpClientConfig(clientConfig);
            DefaultAcsClient client = new DefaultAcsClient(profile);
            return new KmsClient(client);
        }
    
        private KmsClient(DefaultAcsClient acsClient) {
            this.kmsClient = acsClient;
        }
    
        public CreateKeyResponse CreateKey(String keyDesc, String keyUsage) throws ClientException {
            final CreateKeyRequest ckReq = new CreateKeyRequest();
    
            ckReq.setProtocol(ProtocolType.HTTPS);
            ckReq.setAcceptFormat(FormatType.JSON);
            ckReq.setMethod(MethodType.POST);
            ckReq.setDescription(keyDesc);
            ckReq.setKeyUsage(keyUsage);
    
            final CreateKeyResponse response = kmsClient.getAcsResponse(ckReq);
            return response;
        }
    
        public DescribeKeyResponse DescribeKey(String keyId) throws ClientException {
            final DescribeKeyRequest decKeyReq = new DescribeKeyRequest();
    
            decKeyReq.setProtocol(ProtocolType.HTTPS);
            decKeyReq.setAcceptFormat(FormatType.JSON);
            decKeyReq.setMethod(MethodType.POST);
            decKeyReq.setKeyId(keyId);
    
            final DescribeKeyResponse decKeyRes = kmsClient.getAcsResponse(decKeyReq);
            return decKeyRes;
        }
    
        public ListKeysResponse ListKey(int pageNumber, int pageSize) throws ClientException {
            final ListKeysRequest listKeysReq = new ListKeysRequest();
    
            listKeysReq.setProtocol(ProtocolType.HTTPS);
            listKeysReq.setAcceptFormat(FormatType.JSON);
            listKeysReq.setMethod(MethodType.POST);
            listKeysReq.setPageNumber(pageNumber);
            listKeysReq.setPageSize(pageSize);
    
            final ListKeysResponse listKeysRes = kmsClient.getAcsResponse(listKeysReq);
            return listKeysRes;
        }
    
        public GenerateDataKeyResponse GenerateDataKey(String keyId, String keyDesc, int numOfBytes) throws ClientException {
            final  GenerateDataKeyRequest genDKReq = new GenerateDataKeyRequest();
    
            genDKReq.setProtocol(ProtocolType.HTTPS);
            genDKReq.setAcceptFormat(FormatType.JSON);
            genDKReq.setMethod(MethodType.POST);
    
            /**
             * Set parameter according to KMS openAPI document:
             * 1.KeyId
             * 2.KeyDescription
             * 3.NumberOfBytes
             */
            genDKReq.setKeySpec(keyDesc);
            genDKReq.setKeyId(keyId);
            genDKReq.setNumberOfBytes(numOfBytes);
    
            final GenerateDataKeyResponse genDKRes = kmsClient.getAcsResponse(genDKReq);
            return genDKRes;
        }
    
        public EncryptResponse Encrypt(String keyId, String plainText) throws ClientException {
            final EncryptRequest encReq = new EncryptRequest();
    
            encReq.setProtocol(ProtocolType.HTTPS);
            encReq.setAcceptFormat(FormatType.JSON);
            encReq.setMethod(MethodType.POST);
            encReq.setKeyId(keyId);
            encReq.setPlaintext(plainText);
            final EncryptResponse encResponse = kmsClient.getAcsResponse(encReq);
            return encResponse;
        }
    
    
        public DecryptResponse Decrypt(String cipherBlob) throws ClientException {
            final DecryptRequest decReq = new DecryptRequest();
    
            decReq.setProtocol(ProtocolType.HTTPS);
            decReq.setAcceptFormat(FormatType.JSON);
            decReq.setMethod(MethodType.POST);
            decReq.setCiphertextBlob(cipherBlob);
            final DecryptResponse decResponse = kmsClient.getAcsResponse(decReq);
            return decResponse;
        }
    }
    ```

2.  通过KmsClient调用KMS的接口，实现对密钥的枚举、加解密等操作。

    **说明：**

    -   假定您在杭州地域至少有一个KMS主密钥。
    -   `KmsClient.getClientForPublicEndpoint`方法用于初始化KmsClient访问KMS公网接入地址。
    -   `KmsClient.getClientForVpcEndpoint`方法用于初始化KmsClient访问KMS的VPC接入地址。
    ```
    package com.aliyun.kms.samples;
    
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.exceptions.ServerException;
    import com.google.gson.Gson;
    import java.util.*;
    import com.aliyuncs.kms.model.v20160120.*;
    import com.aliyuncs.kms.model.v20160120.ListKeysResponse.Key;
    
    public class KmsSample {
    
     public static void main(String[] args) {
            String accessKeyId = System.getenv("ACCESS_KEY_ID");
            String accessKeySecret = System.getenv("ACCESS_KEY_SECRET");
    
            KmsClient kmsClient = KmsClient.getClientForPublicEndpoint("cn-hangzhou", accessKeyId, accessKeySecret);
            //KmsClient kmsClient = KmsClient.getClientForVpcEndpoint("cn-hangzhou-vpc", accessKeyId, accessKeySecret, "kms-vpc.cn-hangzhou.aliyuncs.com");
            String keyId = null;
            String plainText = "hello world";
            String cipherBlob = null;
    
        /*List all MasterKeys in your account*/
            try {
                final ListKeysResponse listKeysRes = kmsClient.ListKey(1, 100);
    
                /**
                 * Parse response and do more further
                 */
                System.out.println("TotalCount: " + listKeysRes.getTotalCount());
                System.out.println("PageNumber: " + listKeysRes.getPageNumber());
                System.out.println("PageSize: " + listKeysRes.getPageSize());
    
                List<Key> keys = listKeysRes.getKeys();
                Iterator<Key> iterator = keys.iterator();
    
                while (iterator.hasNext()) {
                    keyId = iterator.next().getKeyId();
                    System.out.println("KeyId: " + keyId);
                }
    
                System.out.println("List All MasterKeys success!\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.");
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
    
    
            /*Describe the Key */
            try {
                final DescribeKeyResponse decKeyRes = kmsClient.DescribeKey(keyId);
    
                /**
                 * Parse response and do more further
                 */
                System.out.println("DescribeKey Response: ");
                DescribeKeyResponse.KeyMetadata meta = decKeyRes.getKeyMetadata();
    
                System.out.println("KeyId: " + meta.getKeyId());
                System.out.println("Description: " + meta.getDescription());
                System.out.println("KeyState: " + meta.getKeyState());
                System.out.println("KeyUsage: " + meta.getKeyUsage());
    
                System.out.println("===========================================");
                System.out.println("Describe the MasterKey success!");
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.");
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
    
            /*Generate DataKey*/
            /**
             * Request and got response
             */
            try {
                final GenerateDataKeyResponse genDKResponse = kmsClient.GenerateDataKey(keyId, "AES_256", 64);
    
                /**
                 * Parse response and do more further
                 */
                System.out.println("CiphertextBlob: " + genDKResponse.getCiphertextBlob());
                System.out.println("KeyId: " + genDKResponse.getKeyId());
                System.out.println("Plaintext: " + genDKResponse.getPlaintext());
    
                System.out.println("===========================================");
                System.out.println("Generate DataKey success!");
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.");
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
    
            /**
             * Encrypt the plain text and got a cipher one
             */
            try {
                EncryptResponse encResponse = kmsClient.Encrypt(keyId, plainText);
    
                cipherBlob = encResponse.getCiphertextBlob();
                System.out.println("CiphertextBlob: " + cipherBlob);
                System.out.println("KeyId: " + encResponse.getKeyId());
    
                System.out.println("===========================================");
                System.out.println("Encrypt the plain text success!");
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.");
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
    
            /**
             * Decrypt the cipher text and verify result with original plain text.
             */
            try {
                DecryptResponse decResponse = kmsClient.Decrypt(cipherBlob);
    
                System.out.println("Plaintext: " + decResponse.getPlaintext());
                String verifyPlainText = decResponse.getPlaintext();
                int isMatch = verifyPlainText.compareTo(plainText);
                System.out.println("KeyId: " + decResponse.getKeyId());
                System.out.println("===========================================");
                System.out.printf("Decrypt the cipher text success, result " + (isMatch == 0 ? "match" : "mismatch" + "\n"));
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.");
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
        }
    
     }
                
    ```


