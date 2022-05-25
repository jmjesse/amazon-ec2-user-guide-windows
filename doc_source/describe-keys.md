# Describe public keys<a name="describe-keys"></a>

You can describe the public keys that are stored in Amazon EC2\. You can also retrieve the public key material and identify the public key that was specified at launch\.

**Topics**
+ [Describe public keys](#describe-public-key)
+ [Retrieve the public key material](#retrieving-the-public-key)
+ [Identify the public key specified at launch](#identify-key-pair-specified-at-launch)

## Describe public keys<a name="describe-public-key"></a>

You can view the following information about your public keys that are stored in Amazon EC2: public key name, ID, key type, fingerprint, public key material, the date and time \(in the UTC time zone\) the key was created by Amazon EC2 \(if the key was created by a third\-party tool, then it's the date and time the key was imported to Amazon EC2\), and any tags that are associated with the public key\.

You can use the Amazon EC2 console or AWS CLI to view information about your public keys\.

------
#### [ Console ]

**To view information about your public keys**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the left navigator, choose **Key Pairs**\.

1. You can view the information about each public key in the **Key pairs** table\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/images/key-pairs-describe-console.png)

1. To view a public key's tags, select the check box next to the key, and then choose **Actions**, **Manage tags**\.

------
#### [ AWS CLI ]

**To describe a public key**  
Use the [describe\-key\-pairs](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-key-pairs.html) command and specify the `--key-names` parameter\.

```
aws ec2 describe-key-pairs --key-names my-key-pair
```

Example output

```
{
    "KeyPairs": [
        {
            "KeyPairId": "key-0123456789example",
            "KeyFingerprint": "1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f",
            "KeyName": "my-key-pair",
            "KeyType": "rsa",
            "Tags": [],
            "CreateTime": "2022-04-28T11:37:26.000Z"
        }
    ]
}
```

Alternatively, instead of `--key-names`, you can specify the `--key-pair-ids` parameter to identify the public key\.

```
aws ec2 describe-key-pairs --key-pair-ids key-0123456789example
```

To view the public key material in the output, you must specify the `--include-public-key` parameter\.

```
aws ec2 describe-key-pairs --key-names my-key-pair --include-public-key
```

Example output – In the output, the `PublicKey` field contains the public key material\. 

```
{
    "KeyPairs": [
        {
            "KeyPairId": "key-0123456789example",
            "KeyFingerprint": "1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f",
            "KeyName": "my-key-pair",
            "KeyType": "rsa",
            "Tags": [],
            "PublicKey": "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIj7azlDjVHAsSxgcpCRZ3oWnTm0nAFM64y9jd22ioI/ my-key-pair",
            "CreateTime": "2022-04-28T11:37:26.000Z"
        }
    ]
}
```

------

## Retrieve the public key material<a name="retrieving-the-public-key"></a>

You can use various methods to get access to the public key material\. You can retrieve the public key material from the matching private key on your local computer, or from the instance metadata on the instance that was launched with the public key, or by using the `describe-key-pairs` AWS CLI command\.

Use one of the following methods to retrieve the public key material\.

------
#### [ From the private key ]

**To retrieve the public key material from the private key**  

On your local Windows computer, you can use PuTTYgen to get the public key for your key pair\.

Start PuTTYgen and choose **Load**\. Select the `.ppk` or `.pem` private key file\. PuTTYgen displays the public key under **Public key for pasting into OpenSSH authorized\_keys file**\. You can also view the public key by choosing **Save public key**, specifying a name for the file, saving the file, and then opening the file\.

------
#### [ From the instance metadata ]

You can use Instance Metadata Service Version 2 or Instance Metadata Service Version 1 to retrieve the public key from the instance metadata\.

**Note**  
If you change the key pair that you use to connect to the instance, Amazon EC2 does not update the instance metadata to show the new public key\. The instance metadata continues to show the public key for the key pair that you specified when you launched the instance\.

**To retrieve the public key material from the instance metadata**  
Use one of the following commands from your instance\.

**IMDSv2**

```
PS C:\> [string]$token = Invoke-RestMethod -Headers @{"X-aws-ec2-metadata-token-ttl-seconds" = "21600"} -Method PUT -Uri http://169.254.169.254/latest/api/token
```

```
PS C:\> Invoke-RestMethod -Headers @{"X-aws-ec2-metadata-token" = $token} -Method GET -Uri http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
```

**IMDSv1**

```
PS C:\> Invoke-RestMethod -uri  http://169.254.169.254/latest/meta-data/public-keys/0/openssh-key
```

Example output

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQClKsfkNkuSevGj3eYhCe53pcjqP3maAhDFcvBS7O6V
hz2ItxCih+PnDSUaw+WNQn/mZphTk/a/gU8jEzoOWbkM4yxyb/wB96xbiFveSFJuOp/d6RJhJOI0iBXr
lsLnBItntckiJ7FbtxJMXLvvwJryDUilBMTjYtwB+QhYXUMOzce5Pjz5/i8SeJtjnV3iAoG/cQk+0FzZ
qaeJAAHco+CY/5WrUBkrHmFJr6HcXkvJdWPkYQS3xqC0+FmUZofz221CBt5IMucxXPkX4rWi+z7wB3Rb
BQoQzd8v7yeb7OzlPnWOyN0qFU0XA246RA8QFYiCNYwI3f05p6KLxEXAMPLE my-key-pair
```

For more information about instance metadata, see [Retrieve instance metadata](instancedata-data-retrieval.md)\.

------
#### [ From describe\-key\-pairs ]

**To retrieve the public key material from the `describe-key-pairs`AWS CLI command**  
Use the [describe\-key\-pairs](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-key-pairs.html) command and specify the `--key-names` parameter to identify the public key\. To include the public key material in the output, specify the `--include-public-key` parameter\.

```
aws ec2 describe-key-pairs --key-names my-key-pair --include-public-key
```

Example output – In the output, the `PublicKey` field contains the public key material\. 

```
{
    "KeyPairs": [
        {
            "KeyPairId": "key-0123456789example",
            "KeyFingerprint": "1f:51:ae:28:bf:89:e9:d8:1f:25:5d:37:2d:7d:b8:ca:9f:f5:f1:6f",
            "KeyName": "my-key-pair",
            "KeyType": "rsa",
            "Tags": [],
            "PublicKey": "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIIj7azlDjVHAsSxgcpCRZ3oWnTm0nAFM64y9jd22ioI/ my-key-pair",
            "CreateTime": "2022-04-28T11:37:26.000Z"
        }
    ]
}
```

Alternatively, instead of `--key-names`, you can specify the `--key-pair-ids` parameter to identify the public key\.

```
aws ec2 describe-key-pairs --key-pair-ids key-0123456789example --include-public-key
```

------

## Identify the public key specified at launch<a name="identify-key-pair-specified-at-launch"></a>

If you specify a public key when you launch an instance, the public key name is recorded by the instance\.

**To identify the public key that was specified at launch**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose **Instances**, and then select your instance\.

1. On the **Details** tab, under **Instance details**, the **Key pair name** field displays the name of the public key that you specified when you launched the instance\.

**Note**  
The value of the **Key pair name** field does not change even if you change the public key on the instance, or add public keys\.