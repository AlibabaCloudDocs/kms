# 监控动态RDS凭据轮转

KMS凭据管家支持向云监控投递动态RDS凭据轮转事件，您可以通过云监控的控制台查询轮转事件、创建事件报警，从而实现事件报警、异常事件自动化处理等需求。

## 查询轮转事件

1.  登录[云监控控制台](https://cloudmonitor.console.aliyun.com)。

2.  在左侧导航栏，单击**事件监控**。

3.  在事件监控页面，单击**事件查询**页签。

4.  从下拉列表中选择**密钥管理服务**，然后设置事件类型、事件名称和查询时间段。

5.  在事件列表中找到目标事件，然后单击右侧**操作**列的**查看详情**查询事件详细信息。

    ![轮转](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/1409808061/p201047.png)


## 创建事件报警

您可以创建事件报警，及时了解动态RDS凭据轮转情况，并自动处理异常事件。例如：您可以监控动态RDS凭据轮转失败的事件，通过接入函数计算，自动修复故障。

1.  登录[云监控控制台](https://cloudmonitor.console.aliyun.com)。

2.  在左侧导航栏，单击**事件监控**。

3.  在事件监控页面，单击**报警规则**页签，然后单击**创建事件报警**。

4.  在**创建/修改事件报警**面板，设置以下参数。

    |参数|说明|
    |--|--|
    |**报警规则名称**|报警规则的名称。例如：secrets\_rotation\_failed或secrets\_rotation\_success。|
    |**事件类型**|选择**系统事件**。|
    |**产品类型**|选择**密钥管理服务**。|
    |**事件类型**|报警事件的类型。取值：    -   **异常**：仅对动态RDS凭据轮转失败事件进行报警。
    -   **Notification**：仅对动态RDS凭据轮转成功事件进行报警。
    -   **全部类型**：对所有动态RDS凭据轮转事件进行报警。 |
    |**事件等级**|您需要订阅的事件等级。取值：    -   **严重**：当动态RDS凭据轮转失败时选择该等级。
    -   **信息**：当动态RDS凭据轮转成功时选择该等级。 |
    |**事件名称**|选择您需要消费的事件名称。取值：    -   **托管凭据轮转失败**：仅对动态RDS凭据轮转失败事件进行报警。
    -   **托管凭据轮转成功**：仅对动态RDS凭据轮转成功事件进行报警。
    -   **全部事件**：对所有动态RDS凭据轮转事件进行报警。

**说明：** 不建议您选择**全部事件**，建议您按照事件对业务的影响程度创建不同等级的事件通知。 |
    |**资源范围**|选择**全部资源**。此时任何资源发生相关事件，都会按照配置发送事件通知。|
    |**报警通知**|    -   **联系人组**

默认设置为**云账号报警联系人**。

    -   **通知方式**

取值：

        -   **Warning（短信+邮箱+钉钉机器人）**
        -   **Info（邮箱+钉钉机器人）** |
    |消息处理方式|您可以配置**消息服务队列**、**函数计算**、**URL回调**（GET或POST）或**日志服务**，实现事件的自动化处理。|

5.  单击**确定**。


## 报警通知内容

报警通知的格式为`<资源类型>:<对资源执行的操作>:<执行结果>`。当您为动态RDS凭据轮转事件设置报警后，系统会根据轮转情况为您发送事件报警通知。

-   `Secret:RotateSecret:Failure`：动态RDS凭据轮转失败事件。

    您可以从事件的`content`属性中查看动态RDS凭据轮转事件的相关信息，包括凭据关联的RDS实例ID（`RotationEntityArn`字段），失败的原因（`failureInfo`字段）等。示例代码如下：

    ```
    {
        "product": "KMS",
        "eventTime": "20180816T135935.689+0800",
        "level": "CRITICAL",
        "name": "Secret:RotateSecret:Failure",
        "regionId": "cn-hangzhou",
        "resourceId": " acs:kms:cn-hangzhou:123456789:secret/secretId",
        "status": "Failed",
        "content": {
            "eventId": "eventId",
            "secretName": "SecretName",
            "secretType": "Rds",
            "RotationEntityArn": "acs:rds:$regionId:$accountId:dbinstance/$dbinstanceid",
            "rotationStatus": "Invalid",
            "rotationSubType": "SingleUser",
            "failureInfo": {
                "errorCode": "Kms:ErrorCode",
                "errorMessage": "errorMessage"
            },
            "failureTime": "2012-03-12T05:55:36Z"
        },
        "ver": "1.0"
    }
    ```

-   `Secret:RotateSecret:Success`：动态RDS凭据轮转成功事件。

    示例代码如下：

    ```
    {
        "product":"KMS",
        "instanceName":"secretId", 
        "level":"INFO",
        "name":"Secret:RotateSecret:Success",
        "regionId":"cn-hangzhou",
        "resourceId":" acs:kms:cn-hangzhou:123456789:secret/secretId",
        "status":"Normal",
           "content":{
          "eventId": "eventId",
          "secretName": "SecretName",
          "secretType": "Rds",
          "RotationEntityArn": "acs:rds:$regionId:$accountId:dbinstance/$dbinstanceid",
          "rotationStatus": "Enabled",
          "secretSubType": "SingleUser",
          "successTime": "2012-03-12T05:55:36Z"
        },
        "ver":"1.0"
    }
    ```


