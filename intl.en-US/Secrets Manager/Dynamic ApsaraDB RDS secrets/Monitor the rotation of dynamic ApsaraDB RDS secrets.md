# Monitor the rotation of dynamic ApsaraDB RDS secrets

Secrets Manager can deliver rotation events of dynamic ApsaraDB RDS secrets to Cloud Monitor. You can query the rotation events and create event-triggered alert rules in the Cloud Monitor console. This allows you to receive alert notifications for the events and automate the event handling process.

## Query rotation events

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, click **Event Monitoring**.

3.  On the Event Monitoring page, click the **Query Event** tab.

4.  Select **Key Management Service** from the drop-down list, and then set the event type, event name, and time period to query.

5.  Find the event that you want in the event list, and click **View the Detail** in the **Operation** column to view the event details.


## Create an event-triggered alert rule

You can create event-triggered alert rules to monitor the rotation of dynamic ApsaraDB RDS secrets and automate the event handling process. For example, you can monitor failed rotation of dynamic ApsaraDB RDS secrets and use Function Compute to automatically resolve the failure.

1.  Log on to the [Cloud Monitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, click **Event Monitoring**.

3.  On the Event Monitoring page, click the **Alert Rules** tab. Then, click **Create Event Alert**.

4.  In the **Create / Modify Event Alert** panel, set the parameters that are described in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Alert Rule Name**|The name of the alert rule. Example: secrets\_rotation\_failed or secrets\_rotation\_success.|
    |**Event Type**|Select **System Event**.|
    |**Product Type**|Select **Key Management Service**.|
    |**Event Type**|The type of the alert event. Valid values:    -   **Exception**: Cloud Monitor sends alert notifications only for failed rotation of dynamic ApsaraDB RDS secrets.
    -   **Notification**: Cloud Monitor sends alert notifications only for successful rotation of dynamic ApsaraDB RDS secrets.
    -   **All types**: Cloud Monitor sends alert notifications for all rotation events of dynamic ApsaraDB RDS secrets. |
    |**Event Level**|The level of the events to which you want to subscribe. Valid values:    -   **CRITICAL**: Select this level to subscribe to failed rotation of dynamic ApsaraDB RDS secrets.
    -   **INFO**: Select this level to subscribe to successful rotation of dynamic ApsaraDB RDS secrets. |
    |**Event Name**|Select the name of the event that you want to consume. Valid values:    -   **Secret:RotateSecret:Failure**: Cloud Monitor sends alert notifications only for failed rotation of dynamic ApsaraDB RDS secrets.
    -   **Secret:RotateSecret:Success**: Cloud Monitor sends alert notifications only for successful rotation of dynamic ApsaraDB RDS secrets.
    -   **All Events**: Cloud Monitor sends alert notifications for all rotation events of dynamic ApsaraDB RDS secrets.

**Note:** We recommend that you do not select **All Events**. We recommend that you create different event-triggered alert rules based on the impacts of different events on your business. |
    |**Resource Range**|Select **All Resources**. Cloud Monitor sends alert notifications for events of all resources based on your configurations.|
    |**Alert Notification**|    -   **Contact Group**

By default, **Default Contact Group** is selected.

    -   **Notification Method**

Valid values:

        -   **Warning \(Message+Email ID+DingTalk Robot\)**
        -   **Info \(Email ID+DingTalk Robot\)** |
    |Message processing method|You can configure Message Service \(MNS\) queues, Function Compute, GET or POST URL callbacks, and Log Service to automate the event handling process.|

5.  Click **OK**.


## Alert notification content

An alert notification is in the format of `<Resource type>:<Operation that was performed on the resource>:<Result>`. After you create an event-triggered alert rule for rotation events of dynamic ApsaraDB RDS secrets, the system sends alert notifications based on the rotation result.

-   `Secret:RotateSecret:Failure`: the failed rotation of dynamic ApsaraDB RDS secrets.

    You can view the information about rotation of dynamic ApsaraDB RDS secrets in the `content` field of the event. The information includes the `RotationEntityArn` field that indicates the ID of the ApsaraDB RDS instance associated with the secret and the `failureInfo` field that indicates the failure cause. Sample code:

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

-   `Secret:RotateSecret:Success`: the successful rotation of dynamic ApsaraDB RDS secrets.

    Sample code:

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


