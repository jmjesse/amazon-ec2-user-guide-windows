# Security in Amazon EC2<a name="ec2-security"></a>

Cloud security at AWS is the highest priority\. As an AWS customer, you benefit from a data center and network architecture that are built to meet the requirements of the most security\-sensitive organizations\.

Security is a shared responsibility between AWS and you\. The [shared responsibility model](http://aws.amazon.com/compliance/shared-responsibility-model/) describes this as security of the cloud and security in the cloud:
+ **Security of the cloud** – AWS is responsible for protecting the infrastructure that runs AWS services in the AWS Cloud\. AWS also provides you with services that you can use securely\. Third\-party auditors regularly test and verify the effectiveness of our security as part of the [AWS Compliance Programs](http://aws.amazon.com/compliance/programs/)\. To learn about the compliance programs that apply to Amazon EC2, see [AWS Services in Scope by Compliance Program](http://aws.amazon.com/compliance/services-in-scope/)\.
+ **Security in the cloud** – Your responsibility includes the following areas:
  + Controlling network access to your instances, for example, through configuring your VPC and security groups\. For more information, see [Controlling network traffic](infrastructure-security.md#control-network-traffic)\.
  + Managing the credentials used to connect to your instances\.
  + Managing the guest operating system and software deployed to the guest operating system, including updates and security patches\. For more information, see [Update management in Amazon EC2](update-management.md)\.
  + Configuring the IAM roles that are attached to the instance and the permissions associated with those roles\. For more information, see [IAM roles for Amazon EC2](iam-roles-for-amazon-ec2.md)\.

This documentation helps you understand how to apply the shared responsibility model when using Amazon EC2\. It shows you how to configure Amazon EC2 to meet your security and compliance objectives\. You also learn how to use other AWS services that help you to monitor and secure your Amazon EC2 resources\.

For security best practices for Amazon EC2 running Windows Server, see **Security and Network** under [Best practices for Windows on Amazon EC2](ec2-best-practices.md)\.

**Topics**
+ [Infrastructure security in Amazon EC2](infrastructure-security.md)
+ [Resilience in Amazon EC2](disaster-recovery-resiliency.md)
+ [Data protection in Amazon EC2](data-protection.md)
+ [Identity and access management for Amazon EC2](security-iam.md)
+ [Amazon EC2 key pairs and Windows instances](ec2-key-pairs.md)
+ [Amazon EC2 security groups for Windows instances](ec2-security-groups.md)
+ [Access Amazon EC2 using an interface VPC endpoint](interface-vpc-endpoints.md)
+ [Configuration management in Amazon EC2](configuration-management.md)
+ [Update management in Amazon EC2](update-management.md)
+ [Change management in Amazon EC2](change-management.md)
+ [Compliance validation for Amazon EC2](compliance-validation.md)
+ [Audit and accountability in Amazon EC2](audit-accountability.md)
+ [NitroTPM](nitrotpm.md)