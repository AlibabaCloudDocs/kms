# Secrets Manager JDBC

Secrets Manager JDBC encapsulates business logic, best practices, and design patterns based on dynamic ApsaraDB RDS secrets provided by Secrets Manager. Secrets Manager JDBC allows you to integrate Secrets Manager with your business systems. Secrets Manager JDBC is designed to use dynamic ApsaraDB RDS secrets in database applications. You no longer need to hard code the passwords of database accounts.

## Features

-   Provides common Java Database Connectivity \(JDBC\) drivers and simple database connections.
-   Connects to databases by using c3p0 or Database Connection Pools \(DBCPs\).
-   Allows you to obtain dynamic ApsaraDB RDS secrets by using different access methods. For example, you can use AccessKey pairs, Security Token Service \(STS\), or RAM roles of Elastic Compute Service \(ECS\) instances to obtain dynamic ApsaraDB RDS secrets.
-   Allows you to customize rotation intervals for secrets.

## Limits

-   Only dynamic ApsaraDB RDS secrets are supported. We recommend that you use dynamic ApsaraDB RDS secrets in Manage Dual Account mode. For more information about how to create a dynamic ApsaraDB RDS secret, see [t2005680.md\#section\_tgu\_kh8\_a02](/intl.en-US/Secrets Manager/Dynamic ApsaraDB RDS secrets/Create a dynamic ApsaraDB RDS secret.md).
-   Only Java 1.8 or later is supported.
-   Only ApsaraDB RDS for MySQL, ApsaraDB RDS for SQL Server, ApsaraDB RDS for PostgreSQL, and ApsaraDB RDS for MariaDB instances are supported.

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

**Note:** For more information about the versions of Secrets Manager JDBC, visit [aliyun-secretsmanager-jdbc release](https://github.com/aliyun/aliyun-secretsmanager-jdbc/releases).

## Configure an access method

When Secrets Manager JDBC starts, it checks the secretsmanager.properties file for the access method. The following examples show how to configure different access methods:

-   Obtain dynamic ApsaraDB RDS secrets by using an AccessKey pair

    ```
    ## Specify the access method. 
    credentials_type=ak
    ## Specify the AccessKey ID. 
    credentials_access_key_id=#credentials_access_key_id#
    ## Specify the AccessKey secret. 
    credentials_access_secret=#credentials_access_secret#
    ## Specify the region of Key Management Service (KMS). 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Customize the rotation interval. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```

    **Note:** For more information about how to obtain an AccessKey pair, see [Obtain an AccessKey pair]().

-   Obtain dynamic ApsaraDB RDS secrets by using STS

    ```
    ## Specify the access method. 
    credentials_type=sts
    ## Specify the AccessKey ID. 
    credentials_access_key_id=#credentials_access_key_id#
    ## Specify the AccessKey secret. 
    credentials_access_secret=#credentials_access_secret#
    ## Specify the name of the session for obtaining dynamic ApsaraDB RDS secrets. 
    credentials_role_session_name=#credentials_role_session_name#
    ## Specify the Alibaba Cloud Resource Name (ARN) of the RAM role. 
    credentials_role_arn=#credentials_role_arn#
    ## Specify the policy for obtaining dynamic ApsaraDB RDS secrets. 
    credentials_policy=#credentials_policy#
    ## Specify the region of KMS. 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Customize the rotation interval. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```

    **Note:** For more information about how to obtain an AccessKey pair, see [Obtain an AccessKey pair]().

-   Obtain dynamic ApsaraDB RDS secrets by using a RAM role of an ECS instance

    ```
    ## Specify the access method. 
    credentials_type=ecs_ram_role
    ## Specify the name of the RAM role. 
    credentials_role_name=#credentials_role_name#
    ## Specify the region of KMS. 
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## Customize the rotation interval. The default value is 6 hours. The minimum value is 5 minutes. Unit: milliseconds. 
    refresh_secret_ttl=21600000
    ```

    **Note:** For more information about how to create and authorize a RAM role for an ECS instance, see [Access KMS from an ECS instance in a secure manner](/intl.en-US/Developer Guide/Best practices/Access KMS from an ECS instance in a secure manner.md).


## Sample codes

-   **Access a database by using JDBC**

    The following sample code provides an example on how to access an ApsaraDB RDS for MySQL instance by using JDBC:

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

    The following sample code provides an example of the c3p0.properties configuration file:

    ```
    c3p0.user=#your-mysql-secret-name#
    c3p0.driverClass=com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver
    c3p0.jdbcUrl=secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>
    ```

-   **Access a database by using an open source framework**

    The following sample code provides an example of the Spring configuration file:

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


