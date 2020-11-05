# Sample code for Secrets Manager

This topic provides sample code of KMS SDK for Java to describe how to use a secret created in Secrets Manager. This topic uses the Java SDK as an example to describe how to use a secret.

## Preparations

1.  Obtain the dependency declaration of KMS SDK for Java. For information about the required SDK version, see [SDK overview](/intl.en-US/SDK Reference/SDK overview.md). Example:

    ```
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.2</version>
    </dependency>
    <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-kms</artifactId>
        <version>2.12.0</version>
    </dependency>
    ```

2.  Obtain the endpoints to access KMS based on the region where you use KMS. For more information, see [Endpoints](/intl.en-US/API Reference/Calling method/Request structure.md).

    **Note:** In the example, you can specify the region ID to access the public endpoint of KMS. For more information about how to access the VPC endpoint of KMS, see [SDK code samples](/intl.en-US/SDK Reference/SDK code samples.md).


## Use secrets

You can create a secret to store protected data. For more information, see [Overview](/intl.en-US/User Guide/Secrets Manager/Overview.md).

```
package com.aliyun.kms.secretmanager.samples;

import com.aliyuncs.DefaultAcsClient;
import com.aliyuncs.exceptions.ClientException;
import com.aliyuncs.kms.model.v20160120.*;
import com.aliyuncs.profile.DefaultProfile;
import com.aliyuncs.profile.IClientProfile;
import com.aliyuncs.http.HttpClientConfig;

public class FastUsage {
         /*
          *  Before you access Secrets Manager, assign a permission policy to your access account in the RAM console. For example, assign the AliyunKMSFullAccess policy, which grants management permissions on KMS, to the account. You can also assign system policies or custom policies that grant required permissions on API operations.
          * */
    public static DefaultAcsClient getkmsClient() {
        /*
         *  1. Specify the region where Secrets Manager resides.
         *  2. Specify the AccessKey ID and AccessKey secret that are required to access KMS.
         * */
        IClientProfile profile = DefaultProfile.getProfile("cn-hangzhou","$your_access_key","$your_access_secret");
        HttpClientConfig clientConfig = HttpClientConfig.getDefault();
        profile.setHttpClientConfig(clientConfig);
        return new DefaultAcsClient(profile);
    }


    public static void CreateSecretSample(String secret_name,String secret_data,String version_id) throws ClientException {
        DefaultAcsClient acsClient = getkmsClient();

        CreateSecretRequest req = new CreateSecretRequest();
        req.setSecretName(secret_name);
        req.setSecretData(secret_data);
        req.setVersionId(version_id);
        req.setSecretDataType("text");
        req.setDescription("my app passwd");
        req.setEncryptionKeyId("");           //You can use a symmetric CMK or leave this parameter empty. When this parameter is left empty, you can use the managed key that is created in Secrets Manager.
        req.setTags("");

        CreateSecretResponse rsp = acsClient.getAcsResponse(req);
        System.out.printf("CreateSecret arn: %s; secret_name: %s; versionid: %s; requestid: %s \n",rsp.getArn(),rsp.getSecretName(),rsp.getVersionId(),rsp.getRequestId());
    }


    public static void GetSecretValueSample(String secret_name,String version_stage) throws ClientException {
        DefaultAcsClient acsClient = getkmsClient();

        GetSecretValueRequest req = new GetSecretValueRequest();
        req.setSecretName(secret_name);
        req.setVersionStage(version_stage);

        GetSecretValueResponse  rsp = acsClient.getAcsResponse(req);
        System.out.printf("GetSecretValue  data: %s \n",rsp.getSecretData());
    }



    public static void PutSecretValueSample(String secret_name,String secret_data,String version_id,String version_stages) throws ClientException {
        DefaultAcsClient acsClient = getkmsClient();

        PutSecretValueRequest req = new PutSecretValueRequest();
        req.setSecretName(secret_name);
        req.setSecretData(secret_data);
        req.setSecretDataType("text");
        req.setVersionId(version_id);
        req.setVersionStages(version_stages);  //The secret value of the version that is marked with a specified stage label in the JSON format.


        PutSecretValueResponse rsp = acsClient.getAcsResponse(req);
        System.out.printf("PutSecretValue versionid: %s; now stages: %s \n",rsp.getVersionId(),rsp.getVersionStages());
    }


    public static void DeleteScretSample() throws ClientException {
        DefaultAcsClient acsClient = getkmsClient();

        DeleteSecretRequest req = new DeleteSecretRequest();
        req.setSecretName("myapp_secret");
        req.setForceDeleteWithoutRecovery("true");


        DeleteSecretResponse rsp = acsClient.getAcsResponse(req);
        System.out.printf("DeleteSecret force delete secret:%s \n",rsp.getSecretName());
    }


    public static void main(String[] args ){
        try {
           /*
            *  Create a secret and specify the initial version and the secret value that you want to encrypt. The initial version is marked with ACSCurrent.
            * */
            FastUsage.CreateSecretSample("myapp_secret","mysqpasswdv1","v1");
            /*
             *  Obtain the secret value. If you do not specify a version number or stage label, Secrets Manager returns the secret value of the version marked with ACSCurrent.
             * */
            FastUsage.GetSecretValueSample("myapp_secret","");


            /*
             *  Store the secret value of a new version in the secret and specify VersionStages for this version. If VersionStages is not specified, the version is marked with ACSCurrent.
             * */
            FastUsage.PutSecretValueSample("myapp_secret","mysqpasswdv2","v2","[\"ACSCurrent\", \"MyUserstage\"]");
            /*
             *  Obtain the secret value again. By default, the secret value of the new version is obtained.
             * */
            FastUsage.GetSecretValueSample("myapp_secret","");



            FastUsage.PutSecretValueSample("myapp_secret","mysqpasswdv3","v3","");
            /*
             *  Obtain the secret value. By default, the secret value of the new version is obtained.
             * */
            FastUsage.GetSecretValueSample("myapp_secret","");
            /*
             *  Obtain the secret value. After VersionId or VersionStages is specified, you can obtain the secret value of an earlier version.
             * */
            FastUsage.GetSecretValueSample("myapp_secret","MyUserstage");


            FastUsage.DeleteScretSample();

        } catch (ClientException e) {
            e.printStackTrace();
        }

    }
}
```

For more sample code, see [KMS code development sample library](https://github.com/aliyun/alibabacloud-kms-demo).

