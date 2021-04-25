# Allow applications to access Secrets Manager

Applications can access Secrets Manager by using multiple methods to dynamically use secrets.

## Access methods

Applications can access Secrets Manager by using one of the following methods:

-   [Use KMS SDK](#section_hzp_rfv_3dl)
-   Use Secrets Manager SDK
    -   [Secrets Manager Client](/intl.en-US/Developer Guide/Secrets Manager SDK/Secrets Manager Client.md)

        Secrets Manager Client helps you efficiently use Secrets Manager.

    -   [Secrets Manager JDBC](/intl.en-US/Developer Guide/Secrets Manager SDK/Secrets Manager JDBC.md)

        Secrets Manager JDBC is a Java client that helps you use dynamic ApsaraDB RDS secrets of Secrets Manager to access databases.

-   [Use the Kubernetes plug-in](#section_0vz_zbn_5us)

## Use KMS SDK

This section shows you how to use Key Management Service \(KMS\) SDK for Java to allow applications to use dynamic ApsaraDB RDS secrets. You can also use this method if you use other secrets instead of dynamic ApsaraDB RDS secrets.

1.  Obtain the dependency declaration of KMS SDK for Java.

    For information about the required SDK version, see [SDK overview](/intl.en-US/Developer Guide/KMS SDK/SDK overview.md). Sample code:

    ```
     <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-core</artifactId>
        <version>4.5.16</version>
      </dependency>
      <dependency>
        <groupId>com.aliyun</groupId>
        <artifactId>aliyun-java-sdk-kms</artifactId>
        <version>2.12.0</version>
      </dependency>
      <dependency>
        <groupId>com.alibaba</groupId>
        <artifactId>fastjson</artifactId>
        <version>1.2.9</version>
      </dependency>
      <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.4</version>
      </dependency> 
    ```

2.  Allow applications to obtain the database account and password from Secrets Manager and establish a connection to the database.

    Sample code:

    ```
    package com.aliyun.kms.samples;
    
    import com.alibaba.fastjson.JSON;
    import com.alibaba.fastjson.JSONObject;
    import com.aliyuncs.DefaultAcsClient;
    import com.aliyuncs.exceptions.ClientException;
    import com.aliyuncs.http.FormatType;
    import com.aliyuncs.http.MethodType;
    import com.aliyuncs.http.ProtocolType;
    import com.aliyuncs.kms.model.v20160120.GetSecretValueRequest;
    import com.aliyuncs.kms.model.v20160120.GetSecretValueResponse;
    import com.aliyuncs.profile.DefaultProfile;
    import com.aliyuncs.profile.IClientProfile;
    import org.apache.commons.lang3.tuple.Pair;
    
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.SQLException;
    
    public class RdsSecretSampleCode {
    
        private static final String MYSQL_JDBC_DRIVER = "com.mysql.jdbc.Driver";
        private static final String MSSQL_JDBC_DRIVER = "com.microsoft.sqlserver.jdbc.SQLServerDriver";
    
        private static KmsClient kmsClient;
    
        static {
            kmsClient = KmsClient.getKMSClient("<regionId>", "<accessKeyId>", "<accessKeySecret>");
        }
    
        static class KmsClient {
            private DefaultAcsClient acsClient;
    
            private KmsClient(DefaultAcsClient acsClient) {
                this.acsClient = acsClient;
            }
    
            private static KmsClient getKMSClient(String regionId, String accessKeyId, String accessKeySecret) {
                IClientProfile profile = DefaultProfile.getProfile(regionId, accessKeyId, accessKeySecret);
                DefaultAcsClient client = new DefaultAcsClient(profile);
                return new KmsClient(client);
            }
        }
    
        // Obtain the connection string of the ApsaraDB RDS for MySQL database by using the secret information. 
        public static Connection getMySQLConnectionBySecret(String secretName, String jdbcUrl) throws ClassNotFoundException, SQLException, ClientException {
            Class.forName(MYSQL_JDBC_DRIVER);
            Pair<String, String> userAndPasswordPair = getUserAndPasswordPair(secretName);
            return DriverManager.getConnection(jdbcUrl, userAndPasswordPair.getKey(), userAndPasswordPair.getValue());
        }
    
        // Obtain the connection string of the ApsaraDB RDS for MySQL database by using the secret information. 
        public static Connection getMSSQLConnectionBySecret(String secretName, String jdbcUrl) throws ClassNotFoundException, SQLException, ClientException {
            Class.forName(MSSQL_JDBC_DRIVER);
            Pair<String, String> userAndPasswordPair = getUserAndPasswordPair(secretName);
            return DriverManager.getConnection(jdbcUrl, userAndPasswordPair.getKey(), userAndPasswordPair.getValue());
        }
    
        // Obtains the account and password of the specified database by using the secret information. 
        private static Pair<String, String> getUserAndPasswordPair(String secretName) throws ClientException {
            final GetSecretValueRequest request = new GetSecretValueRequest();
            request.setProtocol(ProtocolType.HTTPS);
            request.setAcceptFormat(FormatType.JSON);
            request.setMethod(MethodType.POST);
            request.setSecretName(secretName);
            GetSecretValueResponse response = kmsClient.acsClient.getAcsResponse(request);
            JSONObject secretDataJSON = JSON.parseObject(response.getSecretData());
            return Pair.of(secretDataJSON.getString("AccountName"), secretDataJSON.getString("AccountPassword"));
        }
    }
    ```


## Use the Kubernetes plug-in

If you use a self-managed Kubernetes cluster or Container Service for Kubernetes \(ACK\) cluster, you can use one of the following methods to integrate Secrets Manager in a codeless way:

-   Install the plug-in by using the ACK console

    1.  Log on to the [ACK console](https://cs.console.aliyun.com).
    2.  In the left-side navigation pane, choose **Marketplace** \> **App Catalog**.
    3.  On the App Catalog page, click the **Alibaba Cloud Apps** tab.
    4.  Enter **ack-secret-manager** in the upper part of the page and click the Search icon.
    5.  Click **ack-secret-manager** to install the plug-in.
    **Note:** You can also visit [ack-secret-manager](https://github.com/AliyunContainerService/ack-secret-manager) and install the plug-in.

-   Install the plug-in by visiting [kubernetes-external-secrets](https://github.com/external-secrets/kubernetes-external-secrets)

The Kubernetes plug-in allows you to configure Secrets Manager as the secret storage. You can specify the name of a secret managed in Secrets Manager. The plug-in reads the latest secret value from Secrets Manager and caches the secret value in the Kubernetes cluster. You can use the dynamic secrets managed in Secrets Manager in the same way as you use Kubernetes secrets.

**Note:** To protect the security of the secrets read from Secrets Manager and other secrets in the Kubernetes cluster, you can encrypt these secrets with a few clicks. For more information, see [Use KMS to encrypt Kubernetes secrets at rest](/intl.en-US/Best Practices/Use KMS to encrypt Kubernetes secrets at rest.md).

