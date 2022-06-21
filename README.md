# VPC with public and private subnets
aws cloud formation template
Adapted from AWS Partner: SAP on AWS Skillbuilder

![architecture](https://github.com/andrewtdunn/public_private_vpc_aws/blob/main/public_private_vpc.drawio.png)

This design pattern is used to create a network environment that has the ability to communicate with both internal (privately routed) and external (publicly routed) resources using a combination of both public and private connections. This design is ideal for SAP workloads that need to accomodate a combination of both public and private routing needs, such as all-in internet-facing, multi-tier web applications supported by databases or other privately routed backend systems. 

<ul>
    <li><h3>Public Subnet</h3>An SAProuter, along with a NAT gateway or NAT instance, are placed in this subnet.<br><br>
    Only the specified public IPs from SAP are allowed to be connected to the SAProuter.
    </li>
    <br>
    <li><h3>Private Subnet</h3>SAP systems reside within the same private subnet. Each of these instances reside within their own security group.</li>
</ul>

### Create stack from aws-cli

```
    aws cloudformation create-stack \
        --stack-name PublicPrivateVPC \ 
        --template-body file://public_private_vpc.yaml \
        --parameters file://parameters.json
```

### Delete stack from aws-cli

```
    aws cloudformation delete-stack --stack-name PublicPrivateVPC 
```
<hr/>

## Networking

1. VPC
    ```
    EnableDnsSupport: true
    EnableDnsHostnames: true
    ```
1. Public Subnet
    ```
    MapPublicIpOnLaunch: true
    ```
1. Internet Gateway
    - Attached to the VPC via IG attachment
1. Public Route Table
    - Associated with the public subnet
    - Default public route to the Internet Gateway
1. Private Subnets
    ```
    MapPublicIpOnLaunch: false
    ```