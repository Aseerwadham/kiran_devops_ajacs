## CLI - Task


* Install and Setup AWS cli on Local machine
* Config PA credentials 
    * aws configure
    * Access key, Secret Key, region, output format

# Create VPC using cli:

   ```aws ec2 create-vpc --cidr-block 10.0.0.0/16```
   ```aws ec2 create-tags --resources vpc-0abcd1234ef56789 --tags Key=Name,Value=MyVPC```

# create Pub and Pvt subnets
   * pub:
   ```aws ec2 create-subnet --vpc-id vpc-0abcd1234ef56789 --cidr-block 10.0.1.0/24 --availability-zone us-east-1a```
   * pri:
   ```aws ec2 create-subnet --vpc-id vpc-0abcd1234ef56789 --cidr-block 10.0.2.0/24 --availability-zone us-east-1b```

# create IGW:
   ```aws ec2 create-internet-gateway```

# Attach IGW to VPC:
   ```aws ec2 attach-internet-gateway --vpc-id vpc-0abcd1234ef56789 --internet-gateway-id igw-0abcd1234ef56789```

# Create Pub and PVT RT:
   * pub:
   ```aws ec2 create-route-table --vpc-id vpc-0abcd1234ef56789```
   * pri:
   ```aws ec2 create-route-table --vpc-id vpc-0abcd1234ef56789```

# Attach Pub sub to Pub rt:
   ```aws ec2 associate-route-table --subnet-id subnet-0abcd1234ef56789 --route-table-id rtb-0abcd1234ef56789```

# Attach Pvt Sub to Pvt rt:
   ```aws ec2 associate-route-table --subnet-id subnet-0abcd1234ef56789 --route-table-id rtb-0abcd1234ef56789```

# Attach IGW to Pub RT:
   ```aws ec2 create-route --route-table-id rtb-0abcd1234ef56789 --destination-cidr-block 0.0.0.0/0 --gateway-id igw-0abcd1234ef56789```

# Create Sg for ssh // http:
```aws ec2 create-security-group --group-name MyPublicSG --description "Allow SSH and HTTP" --vpc-id vpc-0abcd1234ef56789```
```aws ec2 authorize-security-group-ingress --group-id sg-0abcd1234ef56789 --protocol tcp --port 22 --cidr 0.0.0.0/0```
```aws ec2 authorize-security-group-ingress --group-id sg-0abcd1234ef56789 --protocol tcp --port 80 --cidr 0.0.0.0/0```

# Create a Ec2 in Pub Sub:
```aws ec2 run-instances --image-id ami-0abcdef12345 --count 1 --instance-type t2.micro --key-name practice.key --subnet-id subnet-0abcd1234ef56789 --security-group-ids sg-0abcd1234ef56789```

# Create a Ec2 in Pvt Sub:
```aws ec2 run-instances --image-id ami-0abcdef12345 --count 1 --instance-type t2.micro --key-name practice.key --subnet-id subnet-0abcd1234ef56789 --security-group-ids sg-0abcd1234ef56789```
