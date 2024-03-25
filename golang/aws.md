Working with aws-sdk-go-v2 k in golang index of topics wiht links


## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Configuration](#configuration)
- [EC2](#ec2)
- [S3](#s3)
- [DynamoDB](#dynamodb)
- [SQS](#sqs)
- [SNS](#sns)
- [Lambda](#lambda)
- [API Gateway](#api-gateway)
- [IAM](#iam)
- [STS](#sts)
- [CloudWatch](#cloudwatch)
- [CloudTrail](#cloudtrail)
- [CloudFront](#cloudfront)
- [Elastic Beanstalk](#elastic-beanstalk)
- [Elastic Load Balancing](#elastic-load-balancing)
- [Elastic Container Service](#elastic-container-service)
- [Elastic Kubernetes Service](#elastic-kubernetes-service)
- [Elastic File System](#elastic-file-system)
- [Elastic MapReduce](#elastic-mapreduce)
- [Elasticsearch Service](#elasticsearch-service)
- [RDS](#rds)
- [Redshift](#redshift)
- [Athena](#athena)
- [Glue](#glue)
- [Kinesis](#kinesis)
- [Step Functions](#step-functions)
- [Elastic
    Transcoder](#elastic-transcoder)
- [Simple Email Service](#simple-email-service)
- [Simple Notification Service](#simple-notification-service)
- [Simple Queue Service](#simple-queue-service)
- [Simple Workflow Service](#simple-workflow-service)
- [SimpleDB](#simpledb)
- [Cognito](#cognito)
- [API Gateway](#api-gateway)
- [AppSync](#appsync)
- [CloudFormation](#cloudformation)
- [CloudWatch](#cloudwatch)
- [CodeBuild](#codebuild)
- [CodeCommit](#codecommit)
- [CodeDeploy](#codedeploy)
- [CodePipeline](#codepipeline)
- [CodeStar](#codestar)
- [Config](#config)
- [VPC](#vpc)


## Introduction
This document is a collection of links to the official documentation of the AWS SDK for Go. It is intended to be a quick reference for developers who are already familiar with the AWS SDK for Go and want to quickly find information about a specific service or feature.

## Installation
To install the AWS SDK for Go, run the following command:

```bash
go get github.com/aws/aws-sdk-go-v2
```

## Configuration
To configure the AWS SDK for Go, you can use the `aws.Config` struct. Here is an example of how to create a new `aws.Config` struct with the default configuration:

```go
cfg, err := config.LoadDefaultConfig(context.TODO())
if err != nil {
    log.Fatalf("unable to load SDK config, %v", err)
}
```

## EC2
### List all instances
To list all instances in an AWS account, you can use the `DescribeInstances` operation of the `EC2` service client. Here is an example of how to list all instances in an AWS account:

```go
svc := ec2.NewFromConfig(cfg)

result, err := svc.DescribeInstances(context.TODO(), &ec2.DescribeInstancesInput{})
if err != nil {
    log.Fatalf("unable to list instances, %v", err)
}

for _, reservation := range result.Reservations {
    for _, instance := range reservation.Instances {
        fmt.Printf("Instance ID: %s\n", *instance.InstanceId)
    }
}
```

### Get instance by ID
To get an instance by its ID, you can use the `DescribeInstances` operation of the `EC2` service client. Here is an example of how to get an instance by its ID:

```go
svc := ec2.NewFromConfig(cfg)

result, err := svc.DescribeInstances(context.TODO(), &ec2.DescribeInstancesInput{
    InstanceIds: []string{"i-12345678"},
})

if err != nil {
    log.Fatalf("unable to get instance, %v", err)
}

for _, reservation := range result.Reservations {
    for _, instance := range reservation.Instances {
        fmt.Printf("Instance ID: %s\n", *instance.InstanceId)
    }
}
```
### Get instance metadata
To get the metadata of an instance, you can use the `DescribeInstanceMetadata` operation of the `EC2` service client. Here is an example of how to get the metadata of an instance:

```go
svc := ec2.NewFromConfig(cfg)

result, err := svc.DescribeInstanceMetadata(context.TODO(), &ec2.DescribeInstanceMetadataInput{})

if err != nil {
    log.Fatalf("unable to get instance metadata, %v", err)
}

fmt.Printf("Instance ID: %s\n", *result.InstanceId)
```

### Get EC2 Segurite Groups
To get the security groups of an instance, you can use the `DescribeSecurityGroups` operation of the `EC2` service client. Here is an example of how to get the security groups of an instance:

```go
svc := ec2.NewFromConfig(cfg)

result, err := svc.DescribeSecurityGroups(context.TODO(), &ec2.DescribeSecurityGroupsInput{
    GroupIds: []string{"sg-12345678"},
})

if err != nil {
    log.Fatalf("unable to get security groups, %v", err)
}

for _, group := range result.SecurityGroups {
    fmt.Printf("Security Group ID: %s\n", *group.GroupId)
}
```
### Get allowed IP addresses and ports
To get the allowed IP addresses and ports of a security group, you can use the `DescribeSecurityGroupRules` operation of the `EC2` service client. Here is an example of how to get the allowed IP addresses and ports of a security group:

```go
svc := ec2.NewFromConfig(cfg)

result, err := svc.DescribeSecurityGroupRules(context.TODO(), &ec2.DescribeSecurityGroupRulesInput{
    GroupId: aws.String("sg-12345678"),
})

if err != nil {
    log.Fatalf("unable to get security group rules, %v", err)
}

for _, rule := range result.SecurityGroupRules {
    fmt.Printf("Rule ID: %s\n", *rule.RuleId)
}
```

## S3
### List all buckets
To list all buckets in an AWS account, you can use the `ListBuckets` operation of the `S3` service client. Here is an example of how to list all buckets in an AWS account:

```go
svc := s3.NewFromConfig(cfg)

result, err := svc.ListBuckets(context.TODO(), &s3.ListBucketsInput{})
if err != nil {
    log.Fatalf("unable to list buckets, %v", err)
}

for _, bucket := range result.Buckets {
    fmt.Printf("Bucket Name: %s\n", *bucket.Name)
}
```

### Get bucket by name

To get a bucket by its name, you can use the `HeadBucket` operation of the `S3` service client. Here is an example of how to get a bucket by its name:

```go
svc := s3.NewFromConfig(cfg)

_, err := svc.HeadBucket(context.TODO(), &s3.HeadBucketInput{
    Bucket: aws.String("my-bucket"),
})

if err != nil {
    log.Fatalf("unable to get bucket, %v", err)
}

fmt.Printf("Bucket Name: %s\n", "my-bucket")
```

### Get bucket metadata

To get the metadata of a bucket, you can use the `GetBucketMetadata` operation of the `S3` service client. Here is an example of how to get the metadata of a bucket:

```go
svc := s3.NewFromConfig(cfg)

result, err := svc.GetBucketMetadata(context.TODO(), &s3.GetBucketMetadataInput{
    Bucket: aws.String("my-bucket"),
})

if err != nil {
    log.Fatalf("unable to get bucket metadata, %v", err)
}

fmt.Printf("Bucket Name: %s\n", *result.BucketName)
```

### Get bucket policy

To get the policy of a bucket, you can use the `GetBucketPolicy` operation of the `S3` service client. Here is an example of how to get the policy of a bucket:

```go
svc := s3.NewFromConfig(cfg)

result, err := svc.GetBucketPolicy(context.TODO(), &s3.GetBucketPolicyInput{
    Bucket: aws.String("my-bucket"),
})

if err != nil {
    log.Fatalf("unable to get bucket policy, %v", err)
}

fmt.Printf("Bucket Policy: %s\n", *result.Policy)
```

# DynamoDB
### List all tables
To list all tables in a DynamoDB database, you can use the `ListTables` operation of the `DynamoDB` service client. Here is an example of how to list all tables in a DynamoDB database:

```go
svc := dynamodb.NewFromConfig(cfg)

result, err := svc.ListTables(context.TODO(), &dynamodb.ListTablesInput{})
if err != nil {
    log.Fatalf("unable to list tables, %v", err)
}

for _, table := range result.TableNames {
    fmt.Printf("Table Name: %s\n", *table)
}
```

### Get table by name
To get a table by its name, you can use the `DescribeTable` operation of the `DynamoDB` service client. Here is an example of how to get a table by its name:

```go
svc := dynamodb.NewFromConfig(cfg)

result, err := svc.DescribeTable(context.TODO(), &dynamodb.DescribeTableInput{
    TableName: aws.String("my-table"),
})

if err != nil {
    log.Fatalf("unable to get table, %v", err)
}

fmt.Printf("Table Name: %s\n", *result.Table.TableName)
```

### Get table metadata

To get the metadata of a table, you can use the `DescribeTable` operation of the `DynamoDB` service client. Here is an example of how to get the metadata of a table:

```go

svc := dynamodb.NewFromConfig(cfg)

result, err := svc.DescribeTable(context.TODO(), &dynamodb.DescribeTableInput{
    TableName: aws.String("my-table"),
})

if err != nil {
    log.Fatalf("unable to get table metadata, %v", err)
}

fmt.Printf("Table Name: %s\n", *result.Table.TableName)
```

### Get item by key
To get an item by its key, you can use the `GetItem` operation of the `DynamoDB` service client. Here is an example of how to get an item by its key:

```go
svc := dynamodb.NewFromConfig(cfg)

result, err := svc.GetItem(context.TODO(), &dynamodb.GetItemInput{
    TableName: aws.String("my-table"),
    Key: map[string]dynamodb.AttributeValue{
        "id": &dynamodb.AttributeValue{
            S: aws.String("123"),
        },
    },
})

if err != nil {
    log.Fatalf("unable to get item, %v", err)
}

fmt.Printf("Item: %v\n", result.Item)
```

### Put item
To put an item in a table, you can use the `PutItem` operation of the `DynamoDB` service client. Here is an example of how to put an item in a table:

```go
svc := dynamodb.NewFromConfig(cfg)

_, err := svc.PutItem(context.TODO(), &dynamodb.PutItemInput{
    TableName: aws.String("my-table"),
    Item: map[string]dynamodb.AttributeValue{
        "id": &dynamodb.AttributeValue{
            S: aws.String("123"),
        },
        "name": &dynamodb.AttributeValue{
            S: aws.String("John Doe"),
        },
    },
})

if err != nil {
    log.Fatalf("unable to put item, %v", err)
}

fmt.Printf("Item put successfully\n")
```

### Update item
To update an item in a table, you can use the `UpdateItem` operation of the `DynamoDB` service client. Here is an example of how to update an item in a table:

```go
svc := dynamodb.NewFromConfig(cfg)

_, err := svc.UpdateItem(context.TODO(), &dynamodb.UpdateItemInput{
    TableName: aws.String("my-table"),
    Key: map[string]dynamodb.AttributeValue{
        "id": &dynamodb.AttributeValue{
            S: aws.String("123"),
        },
    },
    UpdateExpression: aws.String("SET name = :n"),
    ExpressionAttributeValues: map[string]dynamodb.AttributeValue{
        ":n": &dynamodb.AttributeValue{
            S: aws.String("Jane Doe"),
        },
    },
})

if err != nil {
    log.Fatalf("unable to update item, %v", err)
}

fmt.Printf("Item updated successfully\n")
```

### Delete item
To delete an item from a table, you can use the `DeleteItem` operation of the `DynamoDB` service client. Here is an example of how to delete an item from a table:

```go
svc := dynamodb.NewFromConfig(cfg)

_, err := svc.DeleteItem(context.TODO(), &dynamodb.DeleteItemInput{
    TableName: aws.String("my-table"),
    Key: map[string]dynamodb.AttributeValue{
        "id": &dynamodb.AttributeValue{
            S: aws.String("123"),
        },
    },
})

if err != nil {
    log.Fatalf("unable to delete item, %v", err)
}

fmt.Printf("Item deleted successfully\n")
```

### Query items
To query items in a table, you can use the `Query` operation of the `DynamoDB` service client. Here is an example of how to query items in a table:

```go
svc := dynamodb.NewFromConfig(cfg)

result, err := svc.Query(context.TODO(), &dynamodb.QueryInput{
    TableName: aws.String("my-table"),
    KeyConditionExpression: aws.String("id = :id"),
    ExpressionAttributeValues: map[string]dynamodb.AttributeValue{
        ":id": &dynamodb.AttributeValue{
            S: aws.String("123"),
        },
    },
})

if err != nil {
    log.Fatalf("unable to query items, %v", err)
}

for _, item := range result.Items {
    fmt.Printf("Item: %v\n", item)
}
```

### Scan items
To scan items in a table, you can use the `Scan` operation of the `DynamoDB` service client. Here is an example of how to scan items in a table:

```go
svc := dynamodb.NewFromConfig(cfg)

result, err := svc.Scan(context.TODO(), &dynamodb.ScanInput{
    TableName: aws.String("my-table"),
})

if err != nil {
    log.Fatalf("unable to scan items, %v", err)
}

for _, item := range result.Items {
    fmt.Printf("Item: %v\n", item)
}
```

## SQS
### List all queues
To list all queues in an AWS account, you can use the `ListQueues` operation of the `SQS` service client. Here is an example of how to list all queues in an AWS account:

```go
svc := sqs.NewFromConfig(cfg)

result, err := svc.ListQueues(context.TODO(), &sqs.ListQueuesInput{})
if err != nil {
    log.Fatalf("unable to list queues, %v", err)
}

for _, url := range result.QueueUrls {
    fmt.Printf("Queue URL: %s\n", *url)
}
```

### Get queue URL by name
To get the URL of a queue by its name, you can use the `GetQueueUrl` operation of the `SQS` service client. Here is an example of how to get the URL of a queue by its name:

```go
svc := sqs.NewFromConfig(cfg)

result, err := svc.GetQueueUrl(context.TODO(), &sqs.GetQueueUrlInput{
    QueueName: aws.String("my-queue"),
})

if err != nil {
    log.Fatalf("unable to get queue URL, %v", err)
}

fmt.Printf("Queue URL: %s\n", *result.QueueUrl)
```

### Get queue attributes
To get the attributes of a queue, you can use the `GetQueueAttributes` operation of the `SQS` service client. Here is an example of how to get the attributes of a queue:

```go
svc := sqs.NewFromConfig(cfg)

result, err := svc.GetQueueAttributes(context.TODO(), &sqs.GetQueueAttributesInput{
    QueueUrl: aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
    AttributeNames: []string{"All"},
})

if err != nil {
    log.Fatalf("unable to get queue attributes, %v", err)
}

for key, value := range result.Attributes {
    fmt.Printf("Attribute: %s = %s\n", key, *value)
}
```

### Send message
To send a message to a queue, you can use the `SendMessage` operation of the `SQS` service client. Here is an example of how to send a message to a queue:

```go
svc := sqs.NewFromConfig(cfg)

_, err := svc.SendMessage(context.TODO(), &sqs.SendMessageInput{
    QueueUrl:    aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
    MessageBody: aws.String("Hello, world!"),
})

if err != nil {
    log.Fatalf("unable to send message, %v", err)
}

fmt.Printf("Message sent successfully\n")
```

### Receive message
To receive a message from a queue, you can use the `ReceiveMessage` operation of the `SQS` service client. Here is an example of how to receive a message from a queue:

```go
svc := sqs.NewFromConfig(cfg)

result, err := svc.ReceiveMessage(context.TODO(), &sqs.ReceiveMessageInput{
    QueueUrl: aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
})

if err != nil {
    log.Fatalf("unable to receive message, %v", err)
}

for _, message := range result.Messages {
    fmt.Printf("Message: %s\n", *message.Body)
}
```

### Delete message
To delete a message from a queue, you can use the `DeleteMessage` operation of the `SQS` service client. Here is an example of how to delete a message from a queue:

```go
svc := sqs.NewFromConfig(cfg)

_, err := svc.DeleteMessage(context.TODO(), &sqs.DeleteMessageInput{
    QueueUrl:      aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
    ReceiptHandle: aws.String("AQEBz2Zj7P..."),
})

if err != nil {
    log.Fatalf("unable to delete message, %v", err)
}

fmt.Printf("Message deleted successfully\n")
```

### Reenque message
To reenque a message from a queue, you can use the `ChangeMessageVisibility` operation of the `SQS` service client. Here is an example of how to reenque a message from a queue:

```go
svc := sqs.NewFromConfig(cfg)

_, err := svc.ChangeMessageVisibility(context.TODO(), &sqs.ChangeMessageVisibilityInput{
    QueueUrl:          aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
    ReceiptHandle:     aws.String("AQEBz2Zj7P..."),
    VisibilityTimeout: 0,
})

if err != nil {
    log.Fatalf("unable to reenque message, %v", err)
}

fmt.Printf("Message reenqued successfully\n")
```
### Purge queue
To purge a queue, you can use the `PurgeQueue` operation of the `SQS` service client. Here is an example of how to purge a queue:

```go
svc := sqs.NewFromConfig(cfg)

_, err := svc.PurgeQueue(context.TODO(), &sqs.PurgeQueueInput{
    QueueUrl: aws.String("https://sqs.us-east-1.amazonaws.com/123456789012/my-queue"),
})

if err != nil {
    log.Fatalf("unable to purge queue, %v", err)
}

fmt.Printf("Queue purged successfully\n")
```

## SNS
### List all topics
To list all topics in an AWS account, you can use the `ListTopics` operation of the `SNS` service client. Here is an example of how to list all topics in an AWS account:

```go
svc := sns.NewFromConfig(cfg)

result, err := svc.ListTopics(context.TODO(), &sns.ListTopicsInput{})
if err != nil {
    log.Fatalf("unable to list topics, %v", err)
}

for _, topic := range result.Topics {
    fmt.Printf("Topic ARN: %s\n", *topic.TopicArn)
}
```

### Create topic
To create a topic, you can use the `CreateTopic` operation of the `SNS` service client. Here is an example of how to create a topic:

```go
svc := sns.NewFromConfig(cfg)

result, err := svc.CreateTopic(context.TODO(), &sns.CreateTopicInput{
    Name: aws.String("my-topic"),
})

if err != nil {
    log.Fatalf("unable to create topic, %v", err)
}

fmt.Printf("Topic ARN: %s\n", *result.TopicArn)
```

### Get topic attributes
To get the attributes of a topic, you can use the `GetTopicAttributes` operation of the `SNS` service client. Here is an example of how to get the attributes of a topic:

```go
svc := sns.NewFromConfig(cfg)

result, err := svc.GetTopicAttributes(context.TODO(), &sns.GetTopicAttributesInput{
    TopicArn: aws.String("arn:aws:sns:us-east-1:123456789012:my-topic"),
})

if err != nil {
    log.Fatalf("unable to get topic attributes, %v", err)
}

for key, value := range result.Attributes {
    fmt.Printf("Attribute: %s = %s\n", key, *value)
}
```

### Subscribe to topic
To subscribe to a topic, you can use the `Subscribe` operation of the `SNS` service client. Here is an example of how to subscribe to a topic:

```go
svc := sns.NewFromConfig(cfg)

result, err := svc.Subscribe(context.TODO(), &sns.SubscribeInput{
    TopicArn: aws.String("arn:aws:sns:us-east-1:123456789012:my-topic"),
    Protocol: aws.String("email"),
    Endpoint: aws.String(" [email protected]"),
})

if err != nil {
    log.Fatalf("unable to subscribe to topic, %v", err)
}

fmt.Printf("Subscription ARN: %s\n", *result.SubscriptionArn)
```

### Publish message
To publish a message to a topic, you can use the `Publish` operation of the `SNS` service client. Here is an example of how to publish a message to a topic:

```go
svc := sns.NewFromConfig(cfg)

_, err := svc.Publish(context.TODO(), &sns.PublishInput{
    TopicArn: aws.String("arn:aws:sns:us-east-1:123456789012:my-topic"),
    Message:  aws.String("Hello, world!"),
})

if err != nil {
    log.Fatalf("unable to publish message, %v", err)
}

fmt.Printf("Message published successfully\n")
```







