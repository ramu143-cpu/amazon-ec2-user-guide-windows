# Setting Up<a name="replatform-sql-server-setting-up"></a>

This section covers the steps necessary to run the Windows to Linux replatforming script\.

**Topics**
+ [Prerequisites](#replatform-sql-server-prerequisites)
+ [Prerequisites for Replatforming to an Existing EC2 Instance](#existing-linux-prerequisites)

## Prerequisites<a name="replatform-sql-server-prerequisites"></a>

In order to run the Windows to Linux replatforming assistant for Microsoft SQL Server Databases script, you must:

1. 

**Install the AWS PowerShell Module**

   To install the AWS PowerShell module, follow the steps listed in [Setting up the AWS Tools for PowerShell on a Windows\-Based Computer](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-getting-set-up-windows.html)\. We recommend that you use PowerShell 3\.0 or later for the backup script to work properly\.

1. 

**Install the Windows to Linux Replatforming Assistant PowerShell Backup Script**

   In order to run the Windows to Linux replatforming assistant, download the PowerShell backup script: [https://s3-us-west-1.amazonaws.com/awsec2-server-upgrade-prod/MigrateSQLServerToEC2Linux.ps1](https://s3-us-west-1.amazonaws.com/awsec2-server-upgrade-prod/MigrateSQLServerToEC2Linux.ps1)\.

1. 

**Add an AWS User Profile to the AWS SDK Store**

   To add and configure the AWS user profile, see the steps listed in [Managing Profiles](https://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html#managing-profiles) in the *AWS Tools for PowerShell User Guide*\. [Set the following IAM policy](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-iam-policy.html) for your user profile\. You can also add these permissions as an inline policy under your AWS user account using the IAM console\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
       {
         "Effect": "Allow",
         "Action": [
           "ec2:RebootInstances",
           "ec2:DescribeInstanceStatus",
           "ec2:DescribeInstances",
           "ec2:CreateTags",
           "ec2:RunInstances",
           "ec2:DescribeImages",
           "iam:PassRole",
           "ssm:StartAutomationExecution",
           "ssm:DescribeInstanceInformation",
           "ssm:ListCommandInvocations",
           "ssm:ListCommands",
           "ssm:SendCommand",
           "ssm:GetAutomationExecution",
           "ssm:GetCommandInvocation",
           "s3:PutEncryptionConfiguration",
           "s3:CreateBucket",
           "s3:ListBucket",
           "s3:PutObject",
           "s3:GetObject",
           "s3:DeleteObject",
           "s3:DeleteBucket"
         ],
         "Resource": "*"
       }
     ]
   }
   ```

1. 

**Create an IAM Instance Profile Role**

   To create an IAM instance profile role in order to run Systems Manager on EC2 Linux, see the steps listed under [Create an Instance Profile for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html) in the *AWS Systems Manager User Guide*\.

## Prerequisites for Replatforming to an Existing EC2 Instance<a name="existing-linux-prerequisites"></a>

To replatform to an existing instance running Microsoft SQL Server 2017 on Linux, you must: 

1. Configure the EC2 instance with an AWS Identity and Access Management \(IAM\) profile and attach the `AmazonEC2RoleForSSM` managed policy\. For more information about how to attach a policy to a role, see [Create an Instance Profile for Systems Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html) in the *AWS Systems Manager User Guide*\.

1. Verify that SSM Agent is installed on your EC2 instance\. For more information, see [Installing and Configuring SSM Agent on Amazon EC2 Linux Instances](https://docs.aws.amazon.com/systems-manager/latest/userguide/sysman-install-ssm-agent.html) in the *AWS Systems Manager User Guide*\.

1. Verify that the EC2 instance has enough free disk space to download and restore the Microsoft SQL Server backups\.