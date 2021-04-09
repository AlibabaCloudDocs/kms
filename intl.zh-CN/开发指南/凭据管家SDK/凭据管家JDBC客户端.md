# 凭据管家JDBC客户端

凭据管家JDBC客户端（SecretsManager JDBC）基于KMS凭据管家动态RDS凭据，封装了业务逻辑、最佳实践和设计模式，更易于开发者在业务系统中集成。凭据管家JDBC客户端主要用于在数据库应用中使用动态RDS凭据，告别对数据库账号密码机密信息的硬编码。

## 功能特性

-   提供通用的Java数据库连接JDBC（Java Database Connectivity）驱动，支持简单的数据库连接。
-   通过c3p0和DBCP数据库连接池连接数据库。
-   支持使用AccessKey、STS和ECS实例RAM角色等多种访问方式获取动态RDS凭据。
-   支持用户自定义的凭据刷新频率。

## 使用限制

-   仅支持动态RDS凭据，建议您使用双账号托管的动态RDS凭据。关于如何创建动态RDS凭据，请参见[创建动态RDS凭据](/intl.zh-CN/凭据管家/动态RDS凭据/创建动态RDS凭据.md)。
-   仅支持Java 1.8及以上版本。
-   仅支持MySQL、MSSQL、PostgreSQL和MariaDB四种数据库类型。

## 安装SDK

凭据管家JDBC客户端支持Java语言，您可以访问[凭据管家JDBC开源代码仓库](https://github.com/aliyun/aliyun-secretsmanager-jdbc)了解更多安装信息。

您可以通过Maven的方式安装Java SDK，需要添加的依赖信息如下：

```
<dependency>
    <groupId>com.aliyun</groupId>
    <artifactId>aliyun-secretsmanager-jdbc</artifactId>
    <version>x.x.x</version>
</dependency>
```

**说明：** 凭据管家JDBC客户端具体版本，请参见[alibabacloud-secretsmanager-JDBC-client release](https://github.com/aliyun/aliyun-secretsmanager-jdbc/releases)。

## 配置访问方式

阿里云凭据管家JDBC客户端启动时需要通过解析配置文件（secretsmanager.properties）加载访问方式，不同访问方式的配置文件示例如下：

-   AccessKey访问方式

    ```
    ## 配置访问方式。
    credentials_type=ak
    ## 配置AccessKey ID。
    credentials_access_key_id=#credentials_access_key_id#
    ## 配置AccessKey Secret。
    credentials_access_secret=#credentials_access_secret#
    ## 配置关联的KMS地域。
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## 用户自定义的刷新频率。默认为6小时，最小值为5分钟，单位为毫秒。
    refresh_secret_ttl=21600000
    ```

-   STS访问方式

    ```
    ## 配置访问方式。
    credentials_type=sts
    ## 配置AccessKey ID。
    credentials_access_key_id=#credentials_access_key_id#
    ## 配置AccessKey Secret。
    credentials_access_secret=#credentials_access_secret#
    ## 配置访问凭据Session名称。
    credentials_role_session_name=#credentials_role_session_name#
    ## 配置RAM角色ARN。
    credentials_role_arn=#credentials_role_arn#
    ## 配置访问凭据Policy。
    credentials_policy=#credentials_policy#
    ## 配置关联的KMS地域。
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## 用户自定义的刷新频率。默认为6小时，最小值为5分钟，单位为毫秒。
    refresh_secret_ttl=21600000
    ```

-   ECS实例RAM角色访问方式

    ```
    ## 配置访问方式。
    credentials_type=ecs_ram_role
    ## 配置ECS实例RAM角色名称。
    credentials_role_name=#credentials_role_name#
    ## 配置关联的KMS地域。
    cache_client_region_id=[{"regionId":"#regionId#"}]
    ## 用户自定义的刷新频率。默认为6小时，最小值为5分钟，单位为毫秒。
    refresh_secret_ttl=21600000
    ```


## 示例代码

-   **使用JDBC方式访问数据库**

    使用JDBC方式访问MySQL示例代码如下：

    ```
        Class.forName("com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver");
        Connection connect = null;
        try {
           connect = DriverManager.getConnection("secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>", "#your-mysql-secret-name#","");
        } catch(SQLException e) {
               e.printStackTrace();
        }
    ```

-   **使用数据库连接池c3p0访问数据库**

    配置c3p0配置文件（c3p0.properties）示例代码如下：

    ```
    c3p0.user=#your-mysql-secret-name#
    c3p0.driverClass=com.aliyun.kms.secretsmanager.MysqlSecretsManagerSimpleDriver
    c3p0.jdbcUrl=secrets-manager:mysql://<your-mysql-ip>:<your-mysql-port>/<your-database-name>
    ```

-   **使用数据库开源框架访问数据库**

    配置Spring配置文件示例代码如下：

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


