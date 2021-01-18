# Use ActionTrail to query KMS event logs

Key Management Service \(KMS\) is integrated with ActionTrail. You can use ActionTrail to query the records of all events that are triggered by all users on KMS resources. The users include both Alibaba Cloud accounts and RAM users. This topic describes how to use ActionTrail to query KMS event logs.

ActionTrail records call events for all API operations of KMS, except for the DescribeRegions operation. For more information about the sample code of event logs, see [KMS](/intl.en-US/Event Management/Examples of ActionTrail event logs/KMS.md). For more information about the fields in event logs, see [ActionTrail event log reference](/intl.en-US/Event Management/ActionTrail event log reference.md).

1.  Log on to the [ActionTrail console](https://actiontrail.console.aliyun.com).

2.  In the top navigation bar, select the region where the events that you want to query occurred.

3.  In the left-side navigation pane, choose **ActionTrail** \> **Query Event Details**.

4.  On the Query Event Details page, select **Service Name** from the drop-down list.

    ![Service Name](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6121590161/p225515.png)

5.  Enter **Kms** in the field and click the ![search icon](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7121590161/p225520.png) icon.

    ![Search](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/7121590161/p225519.png)

6.  Move the pointer over the event name in the **Event Name** column to view the event details.

7.  To query the code of an event log, click the plus sign \(+\) to the left of the event record that you want to query. Then, click **Event Detail**.


