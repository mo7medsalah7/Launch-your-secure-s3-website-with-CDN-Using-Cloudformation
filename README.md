# Launch-your-secure-s3-website-with-CDN-Using-Cloudformation


## Theory

**The CloudFormation template will save you time and frustration:**  
1. creates a single S3 bucket with the policy allowing static hosting.
1. creates CloudFront distribution and links the Origin to our s3 bucket.
1. issues and installs the SSL certificate using AWS Certificate Manager.
1. automates all the required Route53 DNS records
1. manages redirects with a CloudFront Function


## Before Deployment.

1. You just need to have the domain purchased and pointed to the hosted zone created for it in AWS Route53 before creating the stack.

1. have AWS CLI installed and a user with AdministratorAccess or you can use the AWS cloudformation console.

## Create the stack using CLI
> **_NOTE:_**  in the template, the Parameter Key = BucketName refers also to your hostedzone name which refers to you domain name.


```
aws cloudformation create-stack \
--stack-name STACK_NAME \
--template-body file://main.yml \
--region us-east-1 \
--parameters ParameterKey=BucketName,ParameterValue=DOMAIN_NAME ParameterKey=HostedZoneId,ParameterValue=HOSTED_ZONE_ID
```

## Deploy your website
Now upload your static website to our created s3 bucket. 

Enter the local directory that contains your website.
```
aws s3 cp ./ s3://BUCKET_NAME_VALUE 

```