## Table of Contents
- [Initial setup commands](#Initial_setup_commands)
- [S3 commands](#s3_commands)
- [Secret Manager Commands](#usage)

## Initial setup commands
```
aws —version
``` 
### List the profiles:
```
aws configure list-profiles
```
### List profile details:
```
aws configure list --profile dev
```
### Configure the profile:
```
aws configure --profile <profile-name>
```
### Login into AWS:
```
aws sso login --profile ssukumar-dev-profile
export AWS_PROFILE=ssukumar-dev-profile
```
---

## S3 commands
### Using profile:
```
aws s3 ls --profile dev
```
### Make Bucket:
```
aws s3 mb s3://radial-test-bucket1/ --profile ssukumar-dev-profile
```
## If the profile is set for the terminal
### List All the buckets:
```
aws s3 ls
```
### Create a new bucket:
```
aws s3 mb s3://radial-test-bucket1/ 
```
### List All files:
```
aws s3 ls s3://radial-test-bucket/
```
### Upload file:
```
echo "Hello from Mac" > test4.txt
aws s3 cp test4.txt  s3://radial-test-bucket/test4.txt
```
### Download the file to local:
```
aws s3 cp s3://radial-test-bucket/test1.txt test1.txt
```
### Remove the file from S3:
```
aws s3 rm s3://radial-test-bucket/test4.txt
```
---
### Check Lambda functions:
```
aws lambda list-functions
```
### Describe API Gateways:
```
aws apigateway get-rest-apis
```
### Create a dummy REST API:
```
aws apigateway create-rest-api --name "TestAPI"
```
### Deploy an API with CLI:
```
aws apigateway create-deployment --rest-api-id <rest-api-id> --stage-name "prod"
```
### Create a simple user pool:
```
aws cognito-idp create-user-pool --pool-name "MyPaymentUserPool"
```
### Create a user pool client:
```
aws cognito-idp create-user-pool-client --user-pool-id <user-pool-id> --client-name "MyWebApp"
```
### Create a CloudFront distribution for a public S3 bucket:
```
aws cloudfront create-distribution \ --origin-domain-name mybucket.s3.amazonaws.com \ --default-root-object index.html
```


> Commands tried during tech tuesday session::
```
chmod 400 "tech_tuesday_001.pem"
ssh -i "tech_tuesday_001.pem" ec2-user@10.96.153.112
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl status httpd
cd /var/www/html
sudo bash -c 'echo "<h1>Hello from My EC2 Web Server</h1><p>Running Apache on AWS</p>" > /var/www/html/index.html'
cat /var/www/html/index.html
sudo tail -f /var/log/httpd/access_log
sudo tail -f /var/log/httpd/error_log
```

### List buckets with CLI:
```
aws s3 ls
```
### Upload a file with CLI:
```
aws s3 cp my-local-file.html s3://<my-s3-bucket-name>/index.html
```
> Commands tried during tech tuesday session:
> Reference: https://docs.aws.amazon.com/cli/latest/reference/s3/#available-commands
```
aws s3 ls
aws s3 mb s3://demo-tech-tuesday-bucket
aws s3 rb s3://demo-tech-tuesday-bucket
aws s3 rb s3://demo-tech-tuesday-bucket --force
### Upload file:
aws s3 cp data.txt s3://demo-tech-tuesday-bucket
### Download file:
aws s3 cp s3://demo-tech-tuesday-bucket .
### List files in a bucket
aws s3 ls s3://demo-tech-tuesday-bucket
```
> Reference: https://docs.aws.amazon.com/cli/latest/reference/s3api/
for the low level S3 commands for the CLI, please see the s3api
Get bucket location:
```
aws s3api get-bucket-location --bucket <bukcet_name>
```

### Create a Lambda function with CLI:
```
aws lambda create-function --function-name "MyNewFunction" --runtime "nodejs18.x" --role <arn-of-iam-role> --handler "index.handler" --zip-file "fileb://my-function.zip"
```
### Invoke a Lambda function with CLI:
```
aws lambda invoke --function-name "MyNewFunction" --payload '{"key1": "value1"}' output.txt
```

### Describe log groups with CLI:
```
aws logs describe-log-groups
```
### Put log events with CLI:
```
aws logs put-log-events --log-group-name "my-log-group" --log-stream-name "my-log-stream" --log-events timestamp=12345,message="Hello World"
```
---
## Secret Manager Commands
AWS Secrets Manager using the AWS CLI:

 1. Create a secret
```
aws secretsmanager create-secret \

  --name MySecretName \

  --description "Demo secret for database password" \

  --secret-string '{"username":"admin","password":"MyP@ssw0rd"}'
```
 

 2. List secrets
```
aws secretsmanager list-secrets
```
 3. Retrieve (get) a secret value
```
aws secretsmanager get-secret-value \

  --secret-id MySecretName

 Output includes both the metadata and the actual secret string:

{

    "ARN": "arn:aws:secretsmanager:us-east-1:123456789012:secret:MySecretName",

    "Name": "MySecretName",

    "SecretString": "{\"username\":\"admin\",\"password\":\"MyP@ssw0rd\"}"

}
```
4. Update a secret 
```
aws secretsmanager update-secret \

  --secret-id MySecretName \

  --secret-string '{"username":"admin","password":"NewP@ssw0rd"}'
```

 5. Delete a secret
```
aws secretsmanager delete-secret \

  --secret-id MySecretName \

  --recovery-window-in-days 7
```
### Create a secret with CLI:
```
aws secretsmanager create-secret --name "MyPaymentDBSecret" --secret-string "{\"username\":\"admin\",\"password\":\"supersecretpassword\"}"
```
### Retrieve a secret with CLI:
```
aws secretsmanager get-secret-value --secret-id "MyPaymentDBSecret"
```
> Commands tried during tech tuesday session:
> https://docs.aws.amazon.com/cli/latest/reference/secretsmanager/
### Create new secret:
```
aws secretsmanager create-secret \
  --name DemoSecret \
  --secret-string '{"username":"admin","password":"Pass123"}'
```
### Get latest secret value
```
aws secretsmanager get-secret-value --secret-id <name>
``` 
### Delete secret (scheduled)
```
aws secretsmanager delete-secret --secret-id <name> --recovery-window-in-days 7
```

### Request a public certificate with CLI:
```
aws acm request-certificate --domain-name "example.com" --validation-method "DNS"
```
### Export a private certificate with CLI:
```
aws acm export-certificate --certificate-arn <certificate-arn> --passphrase "password"
```

