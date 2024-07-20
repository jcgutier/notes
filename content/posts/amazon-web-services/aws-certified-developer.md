---
title: "AWS Certified Developer"
date: 2024-06-22T18:16:00-07:00
---

Content

- [IAM](#iam)
  - [IAM Access Analyzer](#iam-access-analyzer)
  - [Access Advisor feature on IAM console](#access-advisor-feature-on-iam-console)
- [EC2](#ec2)
  - [Dedicated Instances](#dedicated-instances)
  - [Spot Instances](#spot-instances)
  - [Dedicated Hosts](#dedicated-hosts)
  - [On-Demand Instances](#on-demand-instances)
  - [EBS](#ebs)
  - [Autoscaling](#autoscaling)
- [Billing](#billing)
- [RDS](#rds)
  - [Multi-AZ](#multi-az)
- [DynamoDB](#dynamodb)
  - [RCU and WCU](#rcu-and-wcu)
  - [TTL](#ttl)
  - [DAX](#dax)
  - [AWS CLI](#aws-cli)
  - [Transactions](#transactions)
- [API Gateway](#api-gateway)
  - [Usage Plan](#usage-plan)
- [CDK](#cdk)
  - [Constructs](#constructs)
- [Cognito](#cognito)
- [KMS](#kms)
- [S3](#s3)
  - [Encryption](#encryption)
- [VPC](#vpc)
  - [VPC endpoint](#vpc-endpoint)
- [ECS](#ecs)
- [EFS](#efs)
- [CloudFront](#cloudfront)
- [Serverless](#serverless)
  - [AWS Lambda](#aws-lambda)
  - [SAM](#sam)
- [Cloud Watch](#cloud-watch)
- [Elastic Beanstalk](#elastic-beanstalk)
- [SQS](#sqs)
- [API calls](#api-calls)
- [Networking](#networking)
- [AWS CDK](#aws-cdk)
- [ELB](#elb)
- [Elastic Cache](#elastic-cache)
- [Lazy Loading](#lazy-loading)
- [Write-through](#write-through)
- [Adding TTL](#adding-ttl)
- [Secrets Manager](#secrets-manager)
- [APP Sync](#app-sync)
- [Amazon Cognito](#amazon-cognito)
- [Code Commit](#code-commit)
- [Code Deploy](#code-deploy)
- [Cloud Formation](#cloud-formation)
- [x-Ray](#x-ray)
  - [X-Ray sampling](#x-ray-sampling)
  - [EC2 X-Ray Daemon](#ec2-x-ray-daemon)

## IAM

IAM provides the next security tools:

- _IAM Credential Report_: List the accounts users and the status of the credentials
- _IAM Access Advisor_: Shows the permissions granted to a user and when those services were last accessed, this information can be used to revise policies and remove not used permissions.

You manage access in AWS by creating policies and attaching them to IAM identities (users, groups of users, or roles) or AWS resources. A policy is an object in AWS that, when associated with an identity or resource, defines their permissions. Resource-based policies are JSON policy documents that you attach to a resource such as an Amazon S3 bucket. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies.

Trust policy - Trust policies define which principal entities (accounts, users, roles, and federated users) can assume the role. An IAM role is both an identity and a resource that supports resource-based policies. For this reason, you must attach both a trust policy and an identity-based policy to an IAM role. The IAM service supports only one type of resource-based policy called a role trust policy, which is attached to an IAM role.

IAM is used as a certificate manager only when you must support HTTPS connections in a Region that is not supported by ACM. IAM securely encrypts your private keys and stores the encrypted version in IAM SSL certificate storage. IAM supports deploying server certificates in all Regions, but you must obtain your certificate from an external provider for use with AWS. You cannot upload an ACM certificate to IAM. Additionally, you cannot manage your certificates from the IAM Console.

### IAM Access Analyzer

AWS IAM Access Analyzer helps you identify the resources in your organization and accounts, such as Amazon S3 buckets or IAM roles, that are shared with an external entity. This lets you identify unintended access to your resources and data, which is a security risk.

You can set the scope for the analyzer to an organization or an AWS account. This is your zone of trust. The analyzer scans all of the supported resources within your zone of trust. When Access Analyzer finds a policy that allows access to a resource from outside of your zone of trust, it generates an active finding.

### Access Advisor feature on IAM console

Helps identify the unused roles, IAM reports the last-used timestamp that represents when a role was last used to make an AWS request. Your security team can use this information to identify, analyze, and then confidently remove unused roles. This helps improve the security posture of your AWS environments. This does not provide information about non-IAM entities such as S3, hence it's not a correct choice here.

## EC2

Allow to launch virtual machines

If an EC2 instances has been wrongly configured with the 'DeleteOnTermination' attribute set to True for its root EBS volume, the only way to disable this is with the command line by setting the DeleteOnTermination attribute to False

On EC2 you can configure the Amazon CloudWatch agent to stream logs and metrics to CloudWatch. You also can create metric filters from logs that are stored in CloudWatch Logs, this is useful to create metrics from application logs.

### Dedicated Instances

Dedicated Instances are Amazon EC2 instances that run in a virtual private cloud (VPC) on hardware that's dedicated to a single customer. Dedicated Instances that belong to different AWS accounts are physically isolated at a hardware level, even if those accounts are linked to a single-payer account. However, Dedicated Instances may share hardware with other instances from the same AWS account that are not Dedicated Instances.

A Dedicated Host is also a physical server that's dedicated for your use. With a Dedicated Host, you have visibility and control over how instances are placed on the server.


### Spot Instances

A Spot Instance is an unused EC2 instance that is available for less than the On-Demand price. Your Spot Instance runs whenever capacity is available and the maximum price per hour for your request exceeds the Spot price. Any instance present with unused capacity will be allocated. Even though this is cost-effective, it does not fulfill the single-tenant hardware requirement of the client and hence is not the correct option.

### Dedicated Hosts

An Amazon EC2 Dedicated Host is a physical server with EC2 instance capacity fully dedicated to your use. Dedicated Hosts allow you to use your existing software licenses on EC2 instances. With a Dedicated Host, you have visibility and control over how instances are placed on the server. This option is costlier than the Dedicated Instance and hence is not the right choice for the current requirement.

### On-Demand Instances

With On-Demand Instances, you pay for compute capacity by the second with no long-term commitments. You have full control over its lifecycle—you decide when to launch, stop, hibernate, start, reboot, or terminate it. Hardware isolation is not possible and on-demand has one of the costliest instance charges and hence is not the correct answer for current requirements.

### EBS

Is the storage for EC2 over the network, it support in-flight and at rest encryption with KMS, all encrypt/decrypt operations happens on the EC2.

### Autoscaling

A scaling policy instructs Amazon EC2 Auto Scaling to track a specific CloudWatch metric, and it defines what action to take when the associated CloudWatch alarm is in ALARM.

When a scaling policy is executed, if the capacity calculation produces a number outside of the minimum and maximum size range of the group, Amazon EC2 Auto Scaling ensures that the new capacity never goes outside of the minimum and maximum size limits.

Auto Scaling groups cannot span across multiple Regions.

An Auto Scaling group can contain EC2 instances in one or more Availability Zones within the same Region

## Billing

To enable billing for IAM users root user must enable on Profile -> Account -> IAM user and Role Access to Billing information

By default, IAM users do not have access to the AWS Billing and Cost Management console. You or your account administrator must grant users access. You can do this by activating IAM user access to the Billing and Cost Management console and attaching an IAM policy to your users. Then, you need to activate IAM user access for IAM policies to take effect. You only need to activate IAM user access once.

## RDS

Relational database service is a managed service Which provides database engines.

The data is replicated asynchronously to read replicas.

RDS MySQL and RDS PostGreSQL can be configured with IAM Database Authentication

RDS MySQL has storage autoscaling feature.

### Multi-AZ

On RDS multi-AZ, Amazon RDS automatically initiates failover to the standby, in case primary database fails for any reason.

RDS applies OS updates by performing maintenance on the standby, then promoting the standby to primary and finally performing maintenance on the old primary, which becomes the new standby.

On multi-AZ updates are synchronously replicated to the stand-by for disaster recovery.

## DynamoDB

Dynamo DB has the concept of _"streams"_ that will send activities on the tables, like updated, edits, etc.

### RCU and WCU

1 WCU is 1Kb per second.

With strongly consistent reads, 1 RCU is 4 KB per second. With eventually consistent reads, 1 RCU is 4 KB per second and can be made 2 read per second.

RCU and WCU are decoupled, son can be increased/decreased independently. RCUs and WCUs are spread across all the table's partitions.

The maximum size of an item in a DynamoDB table is 400 KB.

### TTL

This field allows for record to be deleted at specific time. This must be activated on table settings.

### DAX

DynamoDB Accelerator (DAX) is a fully managed, highly available, in-memory cache for DynamoDB that delivers up to 10x performance improvement. It caches the most frequently used data, thus offloading the heavy reads on hot keys of your DynamoDB table, hence preventing the "ProvisionedThroughputExceededException" exception.

### AWS CLI

To paginate a _Scan_ operation with AWS CLI the flags: _--max-items_ and _--starting-token__ must be used.

### Transactions

Allow to multiple operation to success only if all of them suceded.

## API Gateway

To mask some fields returned by API gateway backend __Mapping Templates__ must be used.

In API Gateway, an API's method request can take a payload in a different format from the corresponding integration request payload, as required in the backend. Similarly, vice versa is also possible. API Gateway lets you use mapping templates to map the payload from a method request to the corresponding integration request and from an integration response to the corresponding method response.

API Gateway support WebSocket API calls for real time connection.

API Gateway supports the MOCK integration type to return a response without sending the request further to the backend.

To allow only IAM users from another AWS account to access the APIs, we can do: Create an IAM permission policy. Attach the policy to each IAM user. Set the method authorization type for the APIs to AWS_IAM. Use Signature Version 4 to sign the API requests and Create a resource policy for the APIs to allow access for each IAM user only.

With deployment stages in Amazon API Gateway, you can manage multiple release stages for each API. You can configure stage variables so that an API deployment stage can interact with different backend endpoints. You can use API Gateway stage variables to reference a single AWS Lambda function with multiple versions and
aliases.

An Amazon API Gateway Lambda authorizer (formerly known as a custom authorizer) is a Lambda function that you provide to control access to your API. A Lambda authorizer uses bearer token authentication strategies, such as OAuth or SAML. Before creating an API Gateway Lambda authorizer, you must first create the AWS Lambda function that implements the logic to authorize and, if necessary, to authenticate the caller.

API Gateway provides a few strategies for optimizing your API to improve responsiveness, like response caching and payload compression. You can enable API caching in Amazon API Gateway to cache your endpoint's responses.

### Usage Plan

A usage plan specifies who can access one or more deployed API stages and methods—and also how much and how fast they can access them. The plan uses API keys to identify API clients and meters access to the associated API stages for each key.

## CDK

CDK allows to write the infrastructure in a general programming language. CDK builds cloud formation templates.

### Constructs

There 3 level of constructs:

- Layer 1: Resources like from Cloud Formation template
- Layer 2: Resource with some defaults and extra methods
- Layer 3: Bundle of resources with defaults and methods

## Cognito

Cognito have a _post authentication hook_ for AWS Lambda to do any action after a login.

## KMS

KMS service allow to encrypt or decrypt data.

To decrypt data we can use encrypt/decrypt API but only for data less than 4KB. For higher mount of data we should use KMS _GeneratedDataKey_ API.

Envelope encryption is the practice of encrypting plaintext data with a data key and then encrypting the
data key under another key. You must store the encrypted form of the data key so that you can use the data key
to decrypt the encrypted data in the database.

## S3

Which policy condition allows you to enforce SSL requests to objects stored in your S3 bucket? `aws:SecureTransport`

In AWS S3 the max object size is 5TB, if uploading more than 5GB, _multi-part upload_ must be used. But in general if uploading object sizes more than 100MB multi-part upload must be considered.

S3 supports VPC interface endpoint and VPC gateway endpoint.

Amazon S3 Transfer Acceleration, takes advantage of Amazon CloudFront globally distributed edge locations. As the data arrives at an edge location, data is routed to Amazon S3 over an optimized network path. Also this support multipart upload. If the upload is happening on a high-bandwidth network multi-part upload allows to uploading the object parts in parallel with multi-threaded performance, this allow to maximize the usage of available bandwidth.

As an example of multipart upload taken from PhidAssistant:

```python
import boto3

def main():
    # Initialize a session using your AWS credentials
    session = boto3.Session(
        aws_access_key_id='YOUR_ACCESS_KEY',
        aws_secret_access_key='YOUR_SECRET_KEY',
        region_name='us-west-2' # Change this to your desired region
    )

    # Create an S3 client
    s3_client = session.client('s3')

    # The bucket name and file name
    bucket_name = 'your-bucket-name'
    file_name = 'large-file-to-upload.txt'

    # Generate the upload parameters
    part_size = 1024 * 25 # 25 MB
    multipart_upload = s3_client.create_multipart_upload(Bucket=bucket_name, Key=file_name)

    # List of all parts
    uploaded_parts = []

    # Open the file in binary mode
    with open(file_name, 'rb') as data:
        # Calculate the number of parts
        num_of_parts = len(data) // part_size + (len(data) % part_size > 0)
        for in range(num_of_parts):
            # Calculate start and end bytes for each part
            start = i * part_size
            end = min((i+1) * part_size, len(data))
            part_data = data.read(end-start)

            # Upload each part
            response = s3_client.upload_part(
                Body=part_data,
                Bucket=bucket_name,
                Key=file_name,
                PartNumber=i+1,
                UploadId=multipart_upload['UploadId']
            )
            uploaded_parts.append({
                'ETag': response['ETag'],
                'PartNumber': i+1
            })

    # Complete the multipart upload
    s3_client.complete_multipart_upload(
        Bucket=bucket_name,
        Key=file_name,
        UploadId=multipart_upload['UploadId'],
        MultipartUpload={
            'Parts': uploaded_parts
        }
    )

if __name__ == "__main__":
    main()
```

CORS (Cross-origin resource sharing) defines a way or client web applications that are loaded in one domain to interact with resources in a different domain.

To ensure data is encrypted at rest with SSE-S3 using an HTTP API call to upload object, invoke the PutObject API operation and set the x-amz-server-side-encryption header as AES256. Use an S3 bucket policy to deny permission to upload an object unless the request has this header

### Encryption

Object on S3 can be encrypted using 4 methods:

- Server-side encryption (SSE):
  - Server-side encryption with Amazon S3-Managed Keys (SSE-S3) - Enabled by default
  - Server-side encryption with KMS keys stored in AWS KMS (SSE-KMS) - Leverage AWS Key management service to manage encryption keys
  - Server-side encryption with Customer-Provided keys (SSE-C): Manage our owns keys
- Client-side encryption

## VPC

Virtual Private Cloud

### VPC endpoint

VPC endpoints allow communication between instances in the VPC and AWS services with private connection, traffic never leaves AWS network.

## ECS

When using ECS cluster with ASG, the instances have the cluster configuration, like cluster name, in the file `/etc/ecs/ecs.config`, this must be configured on bootstrap

If a container instance is terminated while it is in STOPPED status it will lead to synchronization and it won't be automatically removed from the cluster

If you use a target tracking scaling policy based on a custom Amazon SQS queue metric, dynamic scaling can adjust to the demand curve of your application more effectively. To illustrate with an example, let's say that the current ApproximateNumberOfMessages is 1500 and the fleet's running capacity is 10. If the average processing time is 0.1 seconds for each message and the longest acceptable latency is 10 seconds, then the acceptable backlog per instance is 10 / 0.1, which equals 100. This means that 100 is the target value for your target tracking policy. If the backlog per instance is currently at 150 (1500 / 10), your fleet scales out, and it scales out by five instances to maintain proportion to the target value.

## EFS

Amazon EFS is a file storage service for use with Amazon compute (EC2, containers, serverless) and on-premises servers.

The Standard–IA storage class reduces storage costs for files that are not accessed every day. It

## CloudFront

A signed URL is a URL that provides limited permission and time to make a request.

When you create a signer, the public key is with CloudFront and private key is used to sign a portion of URL - Each signer that you use to create CloudFront signed URLs or signed cookies must have a public–private key pair.

CloudFront signed cookies allow you to control who can access your content when you don't want to change your current URLs or when you want to provide access to multiple restricted files, for example, all of the files in the subscribers' area of a website

When you use the root user to manage CloudFront key pairs, you can only have up to two active CloudFront key pairs per AWS account.

For Amazon CloudFront, you use key pairs to create signed URLs for private content, such as when you want to distribute restricted content that someone paid for.

CloudFront Key Pairs - IAM users can't create CloudFront key pairs. You must log in using root credentials to create key pairs.

To create signed URLs or signed cookies, you need a signer. A signer is either a trusted key group that you create in CloudFront, or an AWS account that contains a CloudFront key pair. AWS recommends that you use trusted key groups with signed URLs and signed cookies instead of using CloudFront key pairs.

## Serverless

AWS Serverless Application Repository (SAR) is a managed repository for serverless applications. It enables teams, organizations, and individual developers to store and share reusable applications, and easily assemble and deploy serverless architectures in powerful new ways.

### AWS Lambda

Memory is the principal lever available to Lambda developers for controlling the performance of a function. You can configure the amount of memory allocated to a Lambda function, between 128 MB and 10,240 MB.
https://photos.google.com/photo/AF1QipO2NattDFKwQyv660gj9AQhYHUu1_mF6sgSf87a
The amount of memory also determines the amount of virtual CPU available to a function. Adding more memory proportionally increases the amount of CPU, increasing the overall computational power available

### SAM

The AWS Serverless Application Model (SAM) is an open-source framework for building serverless applications. It provides shorthand syntax to express functions, APIs, databases, and event source mappings. With just a few lines per resource, you can define the application you want and model it using YAML.

SAM supports the following resource types:

- AWS::Serverless::Api
- AWS::Serverless::Application
- AWS::Serverless::Function
- AWS::Serverless::HttpApi
- AWS::Serverless::LayerVersion
- AWS::Serverless::SimpleTable
- AWS::Serverless::StateMachine

## Cloud Watch

You can publish your own metrics, known as custom metrics, to CloudWatch using the AWS CLI or an API.

Each metric is one of the following:

Standard resolution, with data having a one-minute granularity

High resolution, with data at a granularity of one second

Metrics produced by AWS services are standard resolution by default.

An AWS Lambda function's execution role grants the Lambda function permission to access AWS services and resources. You provide this role when you create a function, and Lambda assumes the role when a function is invoked.

ou can configure an AWS Lambda function to pull in additional code and content in the form of layers. A layer is a .zip file archive that contains libraries, a custom runtime, or other dependencies. With layers, you can use libraries in a Lambda function without needing to include the libraries in a deployment package.

## Elastic Beanstalk

This service offers the next deployment types:

- All at once
- Rolling
- Rolling with an additional batch (This increase the costs as you're adding extra instances during the deployment)
- Immutable
- Traffic splitting

Immutable deployments perform an immutable update to launch a full set of new instances running the new version of the application in a separate Auto Scaling group, alongside the instances running the old version. Immutable deployments can prevent issues caused by partially completed rolling deployments.

Traffic-splitting deployments let you perform canary testing as part of your application deployment. In a traffic-splitting deployment, Elastic Beanstalk launches a full set of new instances just like during an immutable deployment. It then forwards a specified percentage of incoming client traffic to the new application version for a specified evaluation period.

Some policies replace all instances during the deployment or update. This causes all accumulated Amazon EC2 burst balances to be lost. It happens in the following cases:

- Managed platform updates with instance replacement enabled
- Immutable updates
- Deployments with immutable updates or traffic splitting enabled

AWS Elastic Beanstalk makes it easy to create new environments for your application. You can create and manage separate environments for development, testing, and production use, and you can deploy any version of your application to any environment.

Deploy using 'Rolling with additional batch' deployment policy - With this method, Elastic Beanstalk launches an extra batch of instances, then performs a rolling deployment. Launching the extra batch takes time, and ensures that the same bandwidth is retained throughout the deployment. This policy also avoids any reduced availability, although at a cost of an even longer deployment time compared to the Rolling method. Finally, this option is suitable if you must maintain the same bandwidth throughout the deployment.

To configure _Elastic Beanstalk_ for details like provisioning resources or monitoring the configuration muts follow the naming convention:

```bash
.ebextensions/<mysettings>.config
```

## SQS

The minimum message size is 1 byte (1 character). The maximum is 262,144 bytes (256 KB).

You can't change the queue type after you create it and you can't convert an existing standard queue into a FIFO queue.

The visibility timeout value for the queue is defaulted to 30 seconds. Valid values are: An integer from 0 to 43,200 seconds (12 hours).

he dead-letter queue of a FIFO queue must also be a FIFO queue. Similarly, the dead-letter queue of a standard queue must also be a standard queue.

## API calls

DeleteQueue - Deletes the queue specified by the QueueUrl, regardless of the queue's contents. When you delete a queue, any messages in the queue are no longer available.

PurgeQueue - Deletes the messages in a queue specified by the QueueURL parameter. When you use the PurgeQueue action, you can't retrieve any messages deleted from a queue. The queue however remains.

## Networking

Security Groups are stateful, meaning that if incoming traffic port is enabled the communication will be enabled.

Network ACL are stateless, incoming and outgoing traffic must be explicitly allowed for a successful connection. By default NACL does not permit any inbound or outbound connection. To enable the connection to a service running on an instance, the associated network ACL must allow both: 1. Inbound traffic on the port that the service is listening on 2. Outbound traffic to ephemeral ports range (1024-65535).

## AWS CDK

Steps to create an app

Create the app from a template provided by AWS CDK -> Add code to the app to create resources within stacks -> Build the app (optional) -> Synthesize one or more stacks in the app -> Deploy stack(s) to your AWS account

## ELB

A Network Load Balancer functions at the fourth layer of the Open Systems Interconnection (OSI) model. It can handle millions of requests per second. After the load balancer receives a connection request, it selects a target from the target group for the default rule. It attempts to open a TCP connection to the selected target on the port specified in the listener configuration. Incoming connections remain unmodified, so application software need not support X-Forwarded-For.

If an ELB does not have any registered target it will reply with _HTTP 503: Service unavailable_

You must ensure that your load balancer can communicate with registered targets on both the listener port and the health check port. Whenever you add a listener to your load balancer or update the health check port for a target group used by the load balancer to route requests, you must verify that the security groups associated with the load balancer allow traffic on the new port in both directions.

The nodes for a load balancer distribute requests from clients to registered targets. When cross-zone load balancing is enabled, each load balancer node distributes traffic across the registered targets in all enabled Availability Zones. When cross-zone load balancing is disabled, each load balancer node distributes traffic only across the registered targets in its Availability Zone. With Application Load Balancers, cross-zone load balancing is always enabled.

## Elastic Cache

Elastic cache has the following strategies for cache:

## Lazy Loading

Lazy loading is a caching strategy that loads data into the cache only when necessary.

Whenever your application requests data, it first makes the request to the ElastiCache cache. If the data exists in the cache and is current, ElastiCache returns the data to your application. If the data doesn't exist in the cache or has expired, your application requests the data from your data store. Your data store then returns the data to your application. Your application next writes the data received from the store to the cache

## Write-through

The write-through strategy adds data or updates data in the cache whenever data is written to the database.

## Adding TTL

By adding a time to live (TTL) value to each write, you can have the advantages of each _write-through_ and _lazy loading_ strategies. At the same time, you can and largely avoid cluttering up the cache with extra data.

## Secrets Manager

With Secrets Manager, you can rotate, manage, and retrieve database credentials, API keys, and other secrets throughout their lifecycle.

The difference with Systems Manager is that Systems Manager does not automatically rotate credentials.

## APP Sync

AWS AppSync is a managed service that uses GraphQL to help applications get the exact data that they need. You can use AWS AppSync to build scalable applications that require real-time updates on a range of data sources, including Amazon DynamoDB.

## Amazon Cognito

Amazon Cognito adds user sign-up, sign-in, and access control to web and mobile applications. You can also create an AWS Lambda function to make an API call to a custom analytics solution and then invoke that function by using an Amazon Cognito post authentication trigger.

## Code Commit

This service supports the following method for auth:

- SSH keys
- AWS Access Keys
- Git Credentials

## Code Deploy

AWS CodeDeploy is a deployment service that automates application deployments to Amazon EC2 instances, on-premises instances, or serverless Lambda functions. AWS CodeBuild is a fully managed continuous integration service that compiles source code, runs tests, and produces software packages that are ready to deploy.

The blue/green deployment type uses the blue/green deployment model controlled by CodeDeploy. This deployment type enables you to verify a new deployment of service before sending production traffic to it.

## Cloud Formation

Using CloudFormation, you can create a template that describes all the AWS resources that you want (like Amazon EC2 instances or Amazon RDS DB instances), and AWS CloudFormation takes care of provisioning and configuring those resources for you.

A CloudFormation template has an optional Outputs section which declares output values that you can import into other stacks (to create cross-stack references), return in response (to describe stack calls), or view on the AWS CloudFormation console.

Conditions cannot be used within the Parameters section. After you define all your conditions, you can associate them with resources and resource properties only in the Resources and Outputs sections of a template.

he intrinsic function Fn::FindInMap returns the value corresponding to keys in a two-level map that is declared in the Mappings section. YAML Syntax for the full function name: Fn::FindInMap: [ MapName, TopLevelKey, SecondLevelKey ]

Short form of the above syntax is : !FindInMap [ MapName, TopLevelKey, SecondLevelKey ], example:

```
Mappings:
  RegionMap:
    us-east-1:
      HVM64: "ami-0ff8a91507f77f867"
      HVMG2: "ami-0a584ac55a7631c0c"
    us-west-1:
      HVM64: "ami-0bdb828fd58c52235"
      HVMG2: "ami-066ee5fd4a9ef77f1"
    eu-west-1:
      HVM64: "ami-047bb4163c506cd98"
      HVMG2: "ami-31c2f645"
    ap-southeast-1:
      HVM64: "ami-08569b978cc4dfa10"
      HVMG2: "ami-0be9df32ae9f92309"
    ap-northeast-1:
      HVM64: "ami-06cd52961ce9f0d85"
      HVMG2: "ami-053cdd503598e4a9d"
Resources:
  myEC2Instance:
    Type: "AWS::EC2::Instance"
    Properties:
      ImageId: !FindInMap
        - RegionMap
        - !Ref 'AWS::Region'
        - HVM64
      InstanceType: m1.small
```

## x-Ray

### X-Ray sampling

By customizing sampling rules, you can control the amount of data that you record, and modify sampling behavior on the fly without modifying or redeploying your code. Sampling rules tell the X-Ray SDK how many requests to record for a set of criteria. X-Ray SDK applies a sampling algorithm to determine which requests get traced

### EC2 X-Ray Daemon

The AWS X-Ray daemon is a software application that listens for traffic on UDP port 2000, gathers raw segment data, and relays it to the AWS X-Ray API. The daemon logs could help with figuring out the problem.

The X-Ray daemon uses the AWS SDK to upload trace data to X-Ray, and it needs AWS credentials with permission to do that. On Amazon EC2, the daemon uses the instance's instance profile role automatically. Eliminates API permission issues (in case the role doesn't have IAM permissions to write data to the X-Ray service)

Question 56
