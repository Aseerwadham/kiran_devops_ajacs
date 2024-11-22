# Aws - CF - Task


Create the below listed resources, with AWS - Cloudformation !!

- Create VPC using cft
- create Pub and Pvt subnets
- create IGW
- Attach IGW to VPC
- Create Pub and PVT RT
- Attach Pub sub to Pub rt
- Attach Pvt Sub to Pvt rt
- Attach IGW to Pub RT

- Create Sg for ssh // http
- create a key pair for Ec2
- Create a Ec2 in Pub Sub
- Create a Ec2 in Pvt Sub 

```
AWSTemplateFormatVersion: '2010-09-09'
Description: CloudFormation template to create VPC, subnets, routing, security groups, and EC2 instances.

Resources:
  # Create VPC
  AseeVPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsSupport: true
      EnableDnsHostnames: true
      Tags:
        - Key: Name
          Value: AseeVPC

  # Create Internet Gateway
  MyInternetGateway:
    Type: AWS::EC2::InternetGateway
    Properties:
      Tags:
        - Key: Name
          Value: MyInternetGateway

  # Attach IGW to VPC
  AttachGateway:
    Type: AWS::EC2::VPCGatewayAttachment
    Properties:
      VpcId: !Ref AseeVPC
      InternetGatewayId: !Ref MyInternetGateway

  # Create Public Subnet
  PublicSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref AseeVPC
      CidrBlock: 10.0.1.0/24
      MapPublicIpOnLaunch: true
      AvailabilityZone: !Select [0, !GetAZs '']

  # Create Private Subnet
  PrivateSubnet:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref AseeVPC
      CidrBlock: 10.0.2.0/24
      AvailabilityZone: !Select [0, !GetAZs '']

  # Create Public Route Table
  PublicRouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref AseeVPC

  # Create Private Route Table
  PrivateRouteTable:
    Type: AWS::EC2::RouteTable
    Properties:
      VpcId: !Ref AseeVPC

  # Public Route to IGW
  PublicRoute:
    Type: AWS::EC2::Route
    Properties:
      RouteTableId: !Ref PublicRouteTable
      DestinationCidrBlock: 0.0.0.0/0
      GatewayId: !Ref MyInternetGateway

  # Associate Public Subnet with Public Route Table
  PublicSubnetRouteTableAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PublicSubnet
      RouteTableId: !Ref PublicRouteTable

  # Associate Private Subnet with Private Route Table
  PrivateSubnetRouteTableAssociation:
    Type: AWS::EC2::SubnetRouteTableAssociation
    Properties:
      SubnetId: !Ref PrivateSubnet
      RouteTableId: !Ref PrivateRouteTable

  # Create Security Group for SSH and HTTP
  InstanceSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Allow SSH and HTTP access
      VpcId: !Ref AseeVPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 22
          ToPort: 22
          CidrIp: 0.0.0.0/0
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0

  # Create Key Pair
  MyKeyPair:
    Type: AWS::EC2::KeyPair
    Properties:
      KeyName: MyKeyPair

  # Create EC2 Instance in Public Subnet
  PublicEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      KeyName: !Ref MyKeyPair
      SecurityGroupIds:
        - !Ref InstanceSecurityGroup
      SubnetId: !Ref PublicSubnet
      ImageId: ami-0166fe664262f664c 
      Tags:
        - Key: Name
          Value: PublicInstance

  # Create EC2 Instance in Private Subnet
  PrivateEC2Instance:
    Type: AWS::EC2::Instance
    Properties:
      InstanceType: t2.micro
      KeyName: !Ref MyKeyPair
      SecurityGroupIds:
        - !Ref InstanceSecurityGroup
      SubnetId: !Ref PrivateSubnet
      ImageId: ami-0166fe664262f664c
      Tags:
        - Key: Name
          Value: PrivateInstance

Outputs:
  PublicInstancePublicIp:
    Description: Public IP of the Public EC2 Instance
    Value: !GetAtt PublicEC2Instance.PublicIp
  VPCId:
    Description: VPC ID
    Value: !Ref AseeVPC
  PublicSubnetId:
    Description: Public Subnet ID
    Value: !Ref PublicSubnet
  PrivateSubnetId:
    Description: Private Subnet ID
    Value: !Ref PrivateSubnet

```

![preview](Images_folder/cft/image1.png)
![preview](Images_folder/cft/image2.png)
![preview](Images_folder/cft/image3.png)
![preview](Images_folder/cft/image4.png)
![preview](Images_folder/cft/image5.png)
![preview](Images_folder/cft/image6.png)
![preview](Images_folder/cft/image7.png)
![preview](Images_folder/cft/image8.png)
![preview](Images_folder/cft/image9.png)
![preview](Images_folder/cft/image10.png)
![preview](Images_folder/cft/image11.png)
![preview](Images_folder/cft/image12.png)
![preview](Images_folder/cft/image13.png)
![preview](Images_folder/cft/image14.png)
![preview](Images_folder/cft/image15.png)
![preview](Images_folder/cft/image16.png)
![preview](Images_folder/cft/image17.png)
![preview](Images_folder/cft/image18.png)
![preview](Images_folder/cft/image19.png)
![preview](Images_folder/cft/image20.png)
![preview](Images_folder/cft/image21.png)
