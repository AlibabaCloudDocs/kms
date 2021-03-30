# Secrets Manager Client

Secrets Manager Client encapsulates business logic, best practices, and design patterns based on the KMS Secrets Manager API. This allows you to easily integrate these aspects into business systems. You can use Secrets Manager Client to dynamically use the secrets hosted in Secrets Manager. This way, you no longer need to hard code sensitive information.

## Features

Secrets Manager Client provides the following features:

-   Allows you to easily integrate the capabilities of Secrets Manager into applications. You can use a single line of code to read secret information.
-   Allows you to cache and refresh secrets in applications.
-   Encapsulates the API error-based retry mechanism to intelligently handle server errors.
-   Provides a plug-in design mode to allow you to customize features such as extended cache and error retry.

## Install the SDK

Secrets Manager Client SDK is developed in Java. For more information about the SDK, visit the [open source code repository of Secrets Manager](https://github.com/aliyun/alibabacloud-secretsmanager-client-java).

You can add the following Maven dependencies to install Secrets Manager Client SDK for Java:

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>alibabacloud-secretsmanager-client</artifactId>
    <version>x.x.x</version>
</dependency>
```

**Note:** For more information about the versions of Secrets Manager Client, see [alibabacloud-secretsmanager-client release](https://github.com/aliyun/alibabacloud-secretsmanager-client-java/releases).

## Sample code

-   **General code**
    -   Use the environment variables of the system to construct a client:

        ```
        SecretCacheClient client = SecretCacheClientBuilder.newClient();  
        SecretInfo secretInfo = client.getSecretInfo("#secretName#");
        ```

    -   Configure parameters such as an AccessKey ID, AccessKey secret, and region ID to construct a client:

        ```
        SecretCacheClient client = SecretCacheClientBuilder.newCacheClientBuilder(
                  BaseSecretManagerClientBuilder.standard().withCredentialsProvider(CredentialsProviderUtils  
                  .withAccessKey("#accessKeyId#", "#accessKeySecret#")).withRegion("#regionId#").build()).build();  
        SecretInfo secretInfo = client.getSecretInfo("#secretName#");
        ```

-   **Custom code**

    Configure custom parameters to construct a client:

    ```
    SecretCacheClient client = SecretCacheClientBuilder.newCacheClientBuilder(BaseSecretManagerClientBuilder.standard()  
              .withCredentialsProvider(CredentialsProviderUtils.withAccessKey("#accessKeyId#", "#accessKeySecret#"))   
              .withRegion("#regionId#").withBackoffStrategy(new FullJitterBackoffStrategy(3, 2000, 10000)).build())  
              .withCacheSecretStrategy(new FileCacheSecretStoreStrategy("#cacheSecretPath#", true,"#salt#")).withRefreshSecretStrategy(new DefaultRefreshSecretStrategy("#ttlName#"))  
              .withCacheStage("#stage#").withSecretTTL("#secretName#", 1 * 60 * 1000l).withSecretTTL("#secretName1#", 2 * 60 * 1000l).build();  
    SecretInfo secretInfo = client.getSecretInfo("#secretName#");
    ```


