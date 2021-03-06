# Additional Exam Tips

## Based on Student Feedback...

### Kinesis

- Used to consume Big Data
- Stream large amounts of social media, news feeds, logs etc to the cloud
- Think Kinesis when approached with big data questions

- Process large amounts of data;
  - Redshift for business intelligence
  - Elastic Map Reduce for Big Data Processing


### EC2 - EBS Backed Volumes vs Instance Store Volumes

- EBS backed volumes are persistent
- Instance Store backed volumes are not persistent (ephemeral)
- EBS Volumes can be detached and reattached to other EC2 instances

- Instance store volumes cannot be detached and reattached to other instances - they exist only for the life of that instance.
- EBS volumes can be stopped; data will persist

- Instance store volumes cannot be stopped - if you do this the data will be wiped

- EBS Backed = Store Data Long Term
- Instance Store = Shouldn't be used for long-term data storage

### OpsWork

- Orchestration Service that uses Chef
- Chef consists of recipes to maintain a consistent state
- Look for the term "chef" or "recipes" or "cook books" and think OpsWorks

### Elastic Transcoder

- Media Transcoder in the cloud
- Convert media files from their original source format in to different formats that will play on smartphones, tablets, PC's, etc
- Provides transcoding presets for popular output formats, which means that you dont need to guess about which settings work best on particular devices
- Pay based on the minutes that you transcode and the resolution at which you transcode

### SWF Actors

- **Workflow Starter** - An application that can initiate (start) a workflow. Could be your e-commerce website when placing an order or a mobile app searching for bus times.
- **Deciders** - Control the flow of activity tasks in a workflow execution. If something has finished in a workflow (or fails) a Decider decides what to do next.
- **Activity Workers** - Carry out the activity tasks

### EC2 - Get Public IP Address

- Query the instances metadata:
  - `curl http://169.254.169.254/latest/meta-data`
  - `wget http://169.254.169.254/latest/meta-data`
  - Key thing to remember is that its an instances META-DATA, not user data


## Consolidated Billing

### AWS Organizations

AWS Organizations is an account management service that enables you to consolidate multiple AWS accounts into an organization that you create and centrally manage.

Available in 2 feature sets
  - Consolidated Billing
  - All features

**General Rules**

- Paying account is independent
- Cannot access resources of other accounts
- All linked accounts are independent
- Currently a limit of 20 linked accounts - can add more

**Advantages**

- One bill per AWS account
- Very esy to track charges and allocate costs
- Volume Pricing

### Best Practices

- Always enable MFA on root account
- Always use a strong and complex password on root account
- Paying account should be used for billing purposes only. Do not deploy resources in to paying account

### Things to note

- Billing Alerts
  - When monitoring is enabled on the paying account the billing data for all linked accounts is included
  - You can still create billing alerts per indvidual account

- CloudTrail
  - Per AWS Account and is enabled per region

- Can consolidate logs using an S3 bucket
  1. Turn on CloudTrail in the paying account
  2. Create a bucket policy that allows cross account access
  3. Turn on CloudTrail in the other accounts and use the bucket in the paying account

### Tips

- Consolidate billing allows you to get volume discounts on all your accounts.
- Unused reserved instances for EC2 are applied across the group
- CloudTrail is on a per account and per region basis but can be aggregated in to a single bucket in the paynig account.

## Cross Account Access

Many AWS customers use separate AWS accounts for their development and production resources. This separation allows them to cleanly separate different types of resources and can also provide some security benefits.

Cross account access makes it easier for you to work productively within a multi-account (or multi-role) AWS environment by making it easy for you to switch roles within the AWS Management Console.

You can sign in to the console using you IAM user name then switch the console using your IAM user name then switch the console to manage another account without having to enter (or remember) another user name and password

## Resource Groups & Tags

Key Value Pairs attached to AWS resources

Metadata (data about data)

Tags can sometimes be inherited

- Autoscaling, CloudFormation and Elastic Beanstalk can create other resources

Resource groups make it easy to groups your resources using the tags that are assigned to them. You can group that share one or more tags.

**Note: Container for resources**

Resource groups contain information such as:
- Region 
- Name
- Health Checks

Specific Information:
- For EC2 - Public and Private IP Addresses
- For ELB - Port Configurations
- For RDS - Database Engine etc.

## VPC Peering

**Note: Generally not tested in Associate exams, only in Professional exams**

### What is VPC Peering?

VPC Peering is simply a connection bewtween 2 VPCs that enables you to route traffic between them using private IP addresses.

Instances in either VPC can communicate with each other as if they are within the same network. You can create a VPC peering connection between your own VPCs, or with a VPC in another AWS account within a **SINGLE REGION**

AWS uses the existing infrastructure of a VPC to create a VPC peering connection; it is neither a gateway nor a VPN connection, and does not rely on separate piece of physical hardware. There is no single point of failure for communication or bandwidth bottleneck.

### VPC Peering Limitations

1. You cannot create a VPC peering connection between VPCs that have not matching or overlapping CIDR blocks ie. `10.0.0.0/16 -- X --> 10.0.0.0/24`
2. You cannot create a VPC peering connection between VPCs in different regions
3. VPC peering does not support transitive peering relationships.
