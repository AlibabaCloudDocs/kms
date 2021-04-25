# Secrets Manager JDBC

Secrets Manager JDBC encapsulates the business logic, best practices, and design patterns for using dynamic ApsaraDB RDS secrets supported by Secrets Manager. Secrets Manager JDBC allows you to easily integrate Secrets Manager with your business systems. Secrets Manager JDBC is designed to use dynamic ApsaraDB RDS secrets in database applications. This way, you do not need to hardcode the password of a database account.

## Features

-   Provides common Java Database Connectivity \(JDBC\) drivers and supports simple database connections.
-   Connects to databases by using c3p0 or Database Connection Pool \(DBCP\).
-   Allows you to obtain dynamic ApsaraDB RDS secrets by using multiple access methods. For example, you can use AccessKey pairs, Security Token Service \(STS\), or RAM roles of Elastic Compute Service \(ECS\) instances to obtain dynamic ApsaraDB RDS secrets.
-   Allows you to customize the rotation frequency of secrets.

## Limits

-   Only dynamic ApsaraDB RDS secrets are supported. We recommend that you use ApsaraDB RDS secrets in double-account mode. For more information about how to create a dynamic ApsaraDB RDS secret, see [Create a dynamic ApsaraDB RDS secret](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Create a dynamic ApsaraDB RDS secret.md).
-   Only Java 1.8 or later is supported.
-   Only ApsaraDB RDS for MySQL, ApsaraDB RDS for MSSQL, ApsaraDB RDS for PostgreSQL, and ApsaraDB RDS for MariaDB databases are supported.

## Install Secrets Manager JDBC

Secrets Manager JDBC is developed in Java. For more information about how to install Secrets Manager JDBC, visit [aliyun-secretsmanager-jdbc](https://github.com/aliyun/aliyun-secretsmanager-jdbc).

You can install Secrets Manager JDBC by adding the following Maven dependency:

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-secretsmanager-jdbc</artifactId>
    <version>x.x.x</version>
</dependency>
```

**Note:** For more information about the versions of Secrets Manager JDBC, visit [aliyun-secretsmanager-jdbc](https://github.com/aliyun/aliyun-secretsmanager-jdbc/releases).

## Configure the access method

When Secrets Manager JDBC starts, it checks the secretsmanager.properties file for the access method. The following sample configurations show how to configure different access methods.

-   Obtain dynamic ApsaraDB RDS secrets by using an AccessKey pair

    ```
    ## Configure the access method. 
    credentials_type=ak
    ## Configure the AccessKey ID. 
    credentials_access_key_id=#credentials_access_key_id#
    ## Configure the AccessKey secret. 
    credentials_access_secret=#credentials_access_secret#
    ## Configure the region of Key Management Service (KMS). 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Configure the custom rotation frequency. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```

-   Obtain dynamic ApsaraDB RDS secrets by using STS

    ```
    ## Configure the access method. 
    credentials_type=sts
    ## Configure the AccessKey ID. 
    credentials_access_key_id=#credentials_access_key_id#
    ## Configure the AccessKey secret. 
    credentials_access_secret=#credentials_access_secret#
    ## Configure the name of the session for obtaining dynamic ApsaraDB RDS secrets. 
    credentials_role_session_name=#credentials_role_session_name#
    ## Configure the Alibaba Cloud Resource Name (ARN) of the RAM role. 
    credentials_role_arn=#credentials_role_arn#
    ## Configure the policy for obtaining dynamic ApsaraDB RDS secrets. 
    credentials_policy=#credentials_policy#
    ## Configure the region of KMS. 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Configure the custom rotation frequency. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```

-   Obtain dynamic ApsaraDB RDS secrets by using a RAM role of an ECS instance

    ```
    ## Configure the access method. 
    credentials_type=ecs_ram_role
    ## Configure the name of the RAM role. 
    credentials_role_name=#credentials_role_name#
    ## Configure the region of KMS. 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Configure the custom rotation frequency. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```


## Sample code

-   **Access a database by using JDBC**

    The following sample code provides an example on how to access an ApsaraDB RDS for MySQL database by using JDBC:

    ```
        Class.forName("com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver");
        Connection connect = null;
        try {
           connect = DriverManager.getConnection("secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>", "#your-mysql-secret-name#","");
        } catch(SQLException e) {
               e.printStackTrace();
        }
    ```

-   **Access a database by using a c3p0 connection pool**

    The following sample code shows the configuration in the c3p0.properties file:

    ```
    c3p0.user=#your-mysql-secret-name#
    c3p0.driverClass=com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver
    c3p0.jdbcUrl=secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>
    ```

-   **Access a database by using an open source framework**

    The following sample code shows the configuration in the Spring configuration file:

    ```
    <bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" >
          <property name="driverClass" value="com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver" />
          <property name="user" value="#your-mysql-secret-name#" />
          <property name="jdbcUrl" value="secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>" />
          <property name="maxPoolSize" value="500" />
          <property name="minPoolSize" value="5" />
          <property name="initialPoolSize" value="20" />
      </bean>
      <bean id="jdbcTemplate" class="org.springframework.jdbc.core.JdbcTemplate" >
          <property name="dataSource" ref="dataSource" />
      </bean>
    ```


