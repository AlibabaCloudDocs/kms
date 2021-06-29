# Monitor the rotation of dynamic ECS secrets

Secrets Manager can deliver rotation events of dynamic Elastic Compute Service \(ECS\) secrets to CloudMonitor. You can query the rotation events and create event-triggered alert rules in the CloudMonitor console. This allows you to receive alert notifications for the events and automate the event handling process.

## Query rotation events

1.  Log on to the [CloudMonitor console](https://cms-intl.console.aliyun.com).

2.  In the left-side navigation pane, click **Event Monitoring**.

3.  On the Event Monitoring page, click the **Query Event** tab.

4.  Select **Key Management Service** from the drop-down list, and then set the event type, event name, and time period to query.

5.  Find the event that you want to view in the event list and click **View the Detail** in the **Operation** column to view the event details.


## Create an event-triggered alert rule

You can create event-triggered alert rules to monitor the rotation of dynamic ECS secrets and automate the event handling process. For example, you can monitor failed rotation of dynamic ECS secrets and use Function Compute to automatically resolve the failure.

1.  On the Event Monitoring page, click the **Alert Rules** tab. Then, click **Create Event Alert**.

2.  In the **Create / Modify Event Alert** panel, configure the parameters that are described in the following table.

    |Parameter|Description|
    |---------|-----------|
    |**Alert Rule Name**|The name of the alert rule. Example: secrets\_rotation\_failed or secrets\_rotation\_success.|
    |**Event Type**|Select **System Event**.|
    |**Product Type**|Select **Key Management Service**.|
    |**Event Type**|The type of the alert event. Valid values:    -   **Exception**: CloudMonitor sends alert notifications only for failed rotation of dynamic ECS secrets.
    -   **Notification**: CloudMonitor sends alert notifications only for successful rotation of dynamic ECS secrets.
    -   **All types**: CloudMonitor sends alert notifications for all rotation events of dynamic ECS secrets. |
    |**Event Level**|The level of the events to which you want to subscribe. Valid values:    -   **CRITICAL**: Select this level to subscribe to failed rotation of dynamic ECS secrets.
    -   **INFO**: Select this level to subscribe to successful rotation of dynamic ECS secrets. |
    |**Event Name**|Select the name of the event that you want to consume. Valid values:    -   **Secret:RotateSecret:Failure**: CloudMonitor sends alert notifications only for failed rotation of dynamic ECS secrets.
    -   **Secret:RotateSecret:Success**: CloudMonitor sends alert notifications only for successful rotation of dynamic ECS secrets.
    -   **All Events**: CloudMonitor sends alert notifications for all rotation events of dynamic ECS secrets.

**Note:** We recommend that you do not select **All Events**. We recommend that you create different event-triggered alert rules based on the impacts of different events on your business. |
    |**Resource Range**|Select **All Resources**. CloudMonitor sends alert notifications for events of all resources based on your configurations.|
    |**Alert Notification**|    -   **Contact Group**

By default, **Default Contact Group** is selected.

    -   **Notification Method**

Select **Info \(Email ID+DingTalk Robot\)**. |
    |Message processing method|You can configure Message Service \(MNS\) queues, Function Compute, GET or POST URL callbacks, and Log Service to automate the event handling process.|

3.  Click **OK**.


## Alert notification content

An alert notification is in the format of `<Resource type>:<Operation that was performed on the resource>:<Result>`. After you create an event-triggered alert rule for rotation events of dynamic ECS secrets, the system sends alert notifications based on the rotation result.

-   `Secret:RotateSecret:Failure`: the failed rotation of dynamic ECS secrets.

    You can view the information about rotation of dynamic ECS secrets in the `content` field of the event. For example, you can obtain the failure cause by viewing the failureInfo field. Sample code:

    ```
    {
        "product": "KMS",
        "eventTime": "20180816T135935.689+0800",
        "level": "CRITICAL",
        "name": "Secret:RotateSecret:Failure",
        "regionId": "cn-hangzhou",
        "resourceId": "acs:kms:cn-hangzhou:188989715694****:secret/secretName",
        "status": "Failed",
        "content": {
            "eventId": "eventId",
            "secretName": "SecretName",
            "secretType": "ECS",
            "RotationEntityArn": "acs:kms:cn-hangzhou:188989715694****:secret/secretName",
            "rotationStatus": "Invalid",
            "rotationSubType": "Password",
            "failureInfo": {
                "errorCode": "Kms:ErrorCode",
                "errorMessage": "errorMessage"
            },
            "failureTime": "2012-03-12T05:55:36Z"
        },
        "ver": "1.0"
    }
    ```

-   `Secret:RotateSecret:Success`: the successful rotation of dynamic ECS secrets.

    Sample code:

    ```
    {
        "product":"KMS",
        "instanceName":"secretId", 
        "level":"INFO",
        "name":"Secret:RotateSecret:Success",
        "regionId":"cn-hangzhou",
        "resourceId":"acs:kms:cn-hangzhou:188989715694****:secret/secretName",
        "status":"Normal",
           "content":{
          "eventId": "eventId",
          "secretName": "SecretName",
          "secretType": "ECS",
          "RotationEntityArn": "acs:kms:cn-hangzhou:188989715694****:secret/secretName",
          "rotationStatus": "Enabled",
          "secretSubType": "Password",
          "successTime": "2012-03-12T05:55:36Z"
        },
        "ver":"1.0"
    }
    ```


