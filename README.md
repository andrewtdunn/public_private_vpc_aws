# VPC with public and private subnets
aws cloud formation template

![architecture](https://github.com/andrewtdunn/public_private_vpc_aws/blob/main/public_private_vpc.drawio.png)

### Create stack from aws-cli

```
    aws cloudformation create-stack --stack-name PublicPrivateVPC --template-body file://public_private_vpc.yaml --parameters file://parameters.json
```

### Delete stack from aws-cli

```
    aws cloudformation delete-stack --stack-name PublicPrivateVPC 
```