# AWS

## 1. Introduction

AWS architecture can be described with CloudFormation using a simple YAML file:

{% code-tabs %}
{% code-tabs-item title="template.yml" %}
```yaml
Resources:
  Ec2Instance:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: "user5"
      InstanceType: "t2.micro"
      ImageId: "ami-09693313102a30b2c"
      SecurityGroups:
        - !Ref SecurityGroup
  SecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow http to client host
      SecurityGroupIngress:
      - IpProtocol: tcp
        FromPort: 22
        ToPort: 22
        CidrIp: 37.17.221.89/32
      - IpProtocol: tcp
        FromPort: 80
        ToPort: 80
        CidrIp: 37.17.221.89/32
      SecurityGroupEgress:
      - IpProtocol: tcp
        FromPort: 80
        ToPort: 80
        CidrIp: 0.0.0.0/0
  Bucket:
    Type: AWS::S3::Bucket
    Properties:
      AccessControl: String
      AccelerateConfiguration:
        AccelerateConfiguration
      AnalyticsConfigurations:
        - AnalyticsConfiguration
      BucketEncryption:
        BucketEncryption
      BucketName: String
      CorsConfiguration:
        CorsConfiguration
      InventoryConfigurations:
        - InventoryConfiguration
      LifecycleConfiguration:
        LifecycleConfiguration
      LoggingConfiguration:
        LoggingConfiguration
      MetricsConfigurations:
        - MetricsConfiguration
      NotificationConfiguration:
        NotificationConfiguration
    PublicAccessBlockConfiguration:
        PublicAccessBlockConfiguration
      ReplicationConfiguration:
        ReplicationConfiguration
      Tags:
        - Resource Tag
      VersioningConfiguration:
        VersioningConfiguration
      WebsiteConfiguration:
        WebsiteConfiguration
```
{% endcode-tabs-item %}
{% endcode-tabs %}

