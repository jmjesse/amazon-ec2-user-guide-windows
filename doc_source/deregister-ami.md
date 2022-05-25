# Deregister your AMI<a name="deregister-ami"></a>

You can deregister an AMI when you have finished using it\. After you deregister an AMI, you can't use it to launch new instances\.

When you deregister an AMI, it doesn't affect any instances that you've already launched from the AMI or any snapshots created during the AMI creation process\. You'll continue to incur usage costs for these instances and storage costs for the snapshot\. Therefore, you should terminate any instances and delete any snapshots that you're finished with\.

**Topics**
+ [Considerations](#deregister-ami-considerations)
+ [Clean up your AMI](#clean-up-ebs-ami)
+ [Last launched time](#deregister-ami-last-launched-time)

## Considerations<a name="deregister-ami-considerations"></a>

The following considerations apply to deregistering AMIs:
+ You can't deregister an AMI that is not owned by your account\.
+ You can't deregister an AMI that is managed by the AWS Backup service using Amazon EC2\. Instead, use AWS Backup to delete the corresponding recovery points in the backup vault\. For more information, see [Deleting backups](https://docs.aws.amazon.com/aws-backup/latest/devguide/deleting-backups.html) in the *AWS Backup Developer Guide*\.

## Clean up your AMI<a name="clean-up-ebs-ami"></a>

When you deregister an AMI, it doesn't affect the snapshot\(s\) that were created for the volume\(s\) of the instance during the AMI creation process\. You'll continue to incur storage costs for the snapshots\. Therefore, if you are finished with the snapshots, you should delete them\. 

The following diagram illustrates the process for cleaning up your AMI\.

![\[Process to clean up your AMI\]](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/images/ami_delete_ebs.png)

You can use one of the following methods to clean up your AMI\.

------
#### [ New console ]

**To clean up your AMI**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. 

**Deregister the AMI**

   1. In the navigation pane, choose **AMIs**\.

   1. Select the AMI to deregister, and take note of its ID—this can help you find the snapshots to delete in the next step\.

   1. Choose **Actions**, **Deregister AMI**\. When prompted for confirmation, choose **Deregister AMI**\.
**Note**  
It might take a few minutes before the console removes the AMI from the list\. Choose **Refresh** to refresh the status\.

1. 

**Delete snapshots that are no longer needed**

   1. In the navigation pane, choose **Snapshots**\.

   1. Select a snapshot to delete \(look for the AMI ID from the prior step in the **Description** column\)\.

   1. Choose **Actions**, **Delete snapshot**\. When prompted for confirmation, choose **Delete**\.

1. 

**\(Optional\) Terminate instances**  
If you are finished with an instance that you launched from the AMI, you can terminate it\.

   1. In the navigation pane, choose **Instances**, and then select the instance to terminate\.

   1. Choose **Instance state**, **Terminate instance**\. When prompted for confirmation, choose **Terminate**\.

------
#### [ Old console ]

**To clean up your AMI**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. 

**Deregister the AMI**

   1. In the navigation pane, choose **AMIs**\.

   1. Select the AMI to deregister, and take note of its ID — this can help you find the snapshots to delete in the next step\.

   1. Choose **Actions**, **Deregister**\. When prompted for confirmation, choose **Continue**\.
**Note**  
It may take a few minutes before the console removes the AMI from the list\. Choose **Refresh** to refresh the status\.

1. 

**Delete snapshots that are no longer needed**

   1. In the navigation pane, choose **Snapshots**\.

   1. Select a snapshot to delete \(look for the AMI ID from the prior step in the **Description** column\)\.

   1. Choose **Actions**, **Delete**\. When prompted for confirmation, choose **Yes, Delete**\.

1. 

**\(Optional\) Terminate instances**  
If you are finished with an instance that you launched from the AMI, you can terminate it\.

   1. In the navigation pane, choose **Instances**, and then select the instance to terminate\.

   1. Choose **Actions**, **Instance State**, **Terminate**\. When prompted for confirmation, choose **Yes, Terminate**\.

------
#### [ AWS CLI ]

Follow these steps to clean up your AMI

1. 

**Deregister the AMI**

   Deregister the AMI using the [deregister\-image](https://docs.aws.amazon.com/cli/latest/reference/ec2/deregister-image.html) command:

   ```
   aws ec2 deregister-image --image-id ami-12345678
   ```

1. 

**Delete snapshots that are no longer needed**

   Delete snapshots that are no longer needed by using the [delete\-snapshot](https://docs.aws.amazon.com/cli/latest/reference/ec2/delete-snapshot.html) command:

   ```
   aws ec2 delete-snapshot --snapshot-id snap-1234567890abcdef0
   ```

1. 

**Terminate instances \(Optional\)**

   If you are finished with an instance that you launched from the AMI, you can terminate it by using the [terminate\-instances](https://docs.aws.amazon.com/cli/latest/reference/ec2/terminate-instances.html) command:

   ```
   aws ec2 terminate-instances --instance-ids i-12345678
   ```

------
#### [ PowerShell ]

Follow these steps to clean up your AMI

1. 

**Deregister the AMI**

   Deregister the AMI using the [Unregister\-EC2Image](https://docs.aws.amazon.com/powershell/latest/reference/items/Unregister-EC2Image.html) cmdlet:

   ```
   Unregister-EC2Image -ImageId ami-12345678
   ```

1. 

**Delete snapshots that are no longer needed**

   Delete snapshots that are no longer needed by using the [Remove\-EC2Snapshot](https://docs.aws.amazon.com/powershell/latest/reference/items/Remove-EC2Snapshot.html) cmdlet:

   ```
   Remove-EC2Snapshot -SnapshotId snap-12345678
   ```

1. 

**Terminate instances \(Optional\)**

   If you are finished with an instance that you launched from the AMI, you can terminate it by using the [Remove\-EC2Instance](https://docs.aws.amazon.com/powershell/latest/reference/items/Remove-EC2Instance.html) cmdlet:

   ```
   Remove-EC2Instance -InstanceId i-12345678
   ```

------

## Last launched time<a name="deregister-ami-last-launched-time"></a>

`LastLaunchedTime` is a timestamp that indicates when your AMI was last used to launch an instance\. AMIs that have not been used recently might be good candidates for deregistering or [deprecation](ami-deprecate.md)\.

**Note**  
When the AMI is used, there is a 24\-hour delay before that usage is reported\. 
`lastLaunchedTime` data is available starting April 2017\. 

------
#### [ Console ]

**To view the last launched time of an AMI**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the left navigator, choose **AMIs**\.

1. From the filter bar, choose **Owned by me**\.

1. Select the AMI, and then check the **Last launched time** field \(if you selected the check box next to the AMI, it's located on the **Details** tab\)\. The field shows the date and time when the AMI was last used to launch an instance\.

------
#### [ AWS CLI ]

**To view the last launched time of an AMI**  
Run the [describe\-image\-attribute](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-image-attribute.html) command and specify `--attribute lastLaunchedTime`\. You must be the AMI owner to run this command\.

```
aws ec2 describe-image-attribute \
    --image-id ami-1234567890example \
    --attribute lastLaunchedTime
```

Example output

```
{
    "LastLaunchedTime": {
        "Value": "2022-02-10T02:03:18Z"
    },
    "ImageId": "ami-1234567890example",
}
```

------