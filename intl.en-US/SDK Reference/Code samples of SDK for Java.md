# Code samples of SDK for Java

This topic provides some code samples of KMS SDK for Java.

## Background information

-   You can visit the [open source code repository](https://github.com/aliyun/alibabacloud-kms-demo) to view code samples for more programming languages and scenarios. Your valuable comments or code examples would be greatly appreciated.
-   For more information about KMS API operations, see [List of operations by function](/intl.en-US/API Reference/List of operations by function.md).

## Preparations

1.  Obtain the dependency declaration of KMS SDK for Java. For information about the required SDK version, see [SDK overview](/intl.en-US/SDK Reference/SDK overview.md). Sample code:

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

2.  Obtain the endpoints to access KMS based on the region where you use KMS. For more information, see [Endpoints](/intl.en-US/API Reference/Calling method/Request structure.md).

    **Note:** You can access KMS over the Internet or a VPC endpoint. When you use SDK for Java, you must specify parameters based on your business requirements:

    -   If you only specify a region ID, SDK for Java uses the public endpoint of the specified region by default.
    -   If you want to access KMS over a VPC endpoint, you must specify this endpoint.

## Code sample: KmsSample

1.  Create encapsulated class KmsClient:

    ```
    package com.aliyun.kms.samples;
    
    import java.util.*;
    
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http. *;
    
    //Current KMS SDK version:2016-01-20
    import com.aliyuncs.kms.model.v20160120.*;
    import com.aliyuncs.kms.model.v20160120.ListKeysResponse.Key;
    import com.aliyuncs.profile.*;
    
    public class KmsClient
    {
        private DefaultAcsClient kmsClient;
    
        /**
         * Create KmsClient. You need only to specify a region ID. SDK for Java automatically configures the public endpoint of the region.
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
         * Create KmsClient. You can specify a custom endpoint. In most cases, a VPC endpoint is specified.
         */
        public static KmsClient getClientForVpcEndpoint(String regionId, String accessKeyId, String accessKeySecret, String endpoint) {
            //Specify a custom endpoint.
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

2.  Use KmsClient to call KMS API operations to enumerate keys, and encrypt and decrypt data.

    **Note:**

    -   In this code sample, your Alibaba Cloud account has at least one KMS CMK in the China \(Hangzhou\) region.
    -   The `KmsClient.getClientForPublicEndpoint` method is used to initialize KmsClient to access KMS over the public endpoint.
    -   The `KmsClient.getClientForVpcEndpoint` method is used to initialize KmsClient to access KMS over the VPC endpoint.
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
    
                System.out.println("List All MasterKeys success! \n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.") ;
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
                System.out.println("Describe the MasterKey success!") ;
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.") ;
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
                System.out.println("Generate DataKey success!") ;
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.") ;
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
                System.out.println("Encrypt the plain text success!") ;
                System.out.println("===========================================\n");
            } catch (ClientException eResponse) {
                System.out.println("Failed.") ;
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
                System.out.println("Failed.") ;
                System.out.println("Error code: " + eResponse.getErrCode());
                System.out.println("Error message: " + eResponse.getErrMsg());
            }
        }
    
     }
                
    ```


