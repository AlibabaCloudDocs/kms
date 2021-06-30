# Use ActionTrail to query KMS event logs

Key Management Service \(KMS\) is integrated with ActionTrail. You can use ActionTrail to query the logs of all events that are triggered by all users on KMS resources. The users can be Alibaba Cloud accounts or Resource Access Management \(RAM\) users. This topic describes how to use ActionTrail to query KMS event logs.

ActionTrail records call events for all API operations of KMS, except for the DescribeRegions operation. For more information about the sample code to query event logs, see [KMS](/intl.en-US/ActionTrail event log reference/Examples of ActionTrail event logs/KMS.md). For more information about the fields in event logs, see [ActionTrail event log reference](/intl.en-US/ActionTrail event log reference/ActionTrail event log reference.md).

1.  Log on to the [ActionTrail console](https://actiontrail.console.aliyun.com).

2.  In the left-side navigation pane, click **Event Detail Query**.

3.  In the top navigation bar, select the region of the events that you want to query.

4.  On the Event Detail Query page, select **Service Name** from the drop-down list.

5.  Enter **Kms** in the field and click the ![search](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/6718105261/p290286.png) icon.

6.  Move the pointer over an event name in the **Event Name** column to view the details of the event.

7.  If you want to query the code records of an event, click the plus sign \(+\) to the left of the event name. Then, click **Event Detail**.


