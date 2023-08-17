# EC2_Tutorial_Documentation
*Documentation of the process of running an EC2 instance in AWS CLI and CloudFormation.*

## Former2 Diagram
<details>
![alt text](https://github.com/SkyOfSteel/EC2_Tutorial_Documentation/blob/main/EC2%20Tutorial%20Instance.png?raw=true)

The code to add an image link from the repo is:

```
![alt text](https://github.com/SkyOfSteel/EC2_Tutorial_Documentation/blob/main/EC2%20Tutorial%20Instance.png?raw=true)
```
</details>

## AWS CLI Command
<details>
```
aws ec2 run-instances --image-id ami-0453898e98046c639 --count 1 --instance-type t2.micro --key-name "EC2 Tutorial" --security-group-ids sg-0588aaba70932e8b6 --subnet-id subnet-0d8164236d978a1e5

aws ec2 create-tags --resources i-06eab29402aaf2854 --tags Key=Name,Value=Test-Instance,Key=Description,Value="This is a test instance."
```

Where **--image-id** is the standard ID for Amazon's own Amazon Linux 2 AMI.

*My AWS Configure default region is different from the region where the instance was created, so an additional command is required to list it in the console.*

```
aws --region us-east-1 ec2 describe-instances
```
</details>

## CloudFormation Template
*The file is available in the repository.*
<details>
```
AWSTemplateFormatVersion: "2010-09-09"
Metadata:
    Generator: "former2"
Description: ""
Resources:
    EC2Instance:
        Type: "AWS::EC2::Instance"
        Properties:
            ImageId: "ami-0453898e98046c639"
            InstanceType: "t2.micro"
            KeyName: "EC2 Tutorial"
            AvailabilityZone: !Sub "${AWS::Region}d"
            Tenancy: "default"
            SubnetId: "subnet-0d8164236d978a1e5"
            EbsOptimized: false
            SecurityGroupIds: 
              - "sg-0588aaba70932e8b6"
            SourceDestCheck: true
            BlockDeviceMappings: 
              - 
                DeviceName: "/dev/xvda"
                Ebs: 
                    Encrypted: false
                    VolumeSize: 8
                    SnapshotId: "snap-05e7955c47c599709"
                    VolumeType: "gp2"
                    DeleteOnTermination: true
            UserData: "IyEvYmluL2Jhc2gKIyBVc2UgdGhpcyBmb3IgeW91ciB1c2VyIGRhdGEgKHNjcmlwdCBmcm9tIHRvcCB0byBib3R0b20pCiMgaW5zdGFsbCBodHRwZCAoTGludXggMiB2ZXJzaW9uKQp5dW0gdXBkYXRlIC15Cnl1bSBpbnN0YWxsIC15IGh0dHBkCnN5c3RlbWN0bCBzdGFydCBodHRwZApzeXN0ZW1jdGwgZW5hYmxlIGh0dHBkCmVjaG8gIjxoMT5IZWxsbyBXb3JsZCBmcm9tICQoaG9zdG5hbWUgLWYpPC9oMT4iID4gL3Zhci93d3cvaHRtbC9pbmRleC5odG1s"
            Tags: 
              - 
                Key: "Description"
                Value: "This is a test instance."
              - 
                Key: "Name"
                Value: "Test-Instance"
            HibernationOptions: 
                Configured: false
            EnclaveOptions: 
                Enabled: false
```
</details>