
## 📌 AWS CLI Commands Cheat Sheet

<details>
  <summary><strong>📑 Table of Contents (Click to Expand)</strong></summary>

- [Initial Setup Commands](#initial-setup-commands)
- [S3 Commands](#s3-commands)
- [Lambda Commands](#lambda-commands)
- [API Gateway Commands](#api-gateway-commands)
- [Cognito Commands](#cognito-commands)
- [CloudFront Commands](#cloudfront-commands)
- [CloudWatch Logs Commands](#cloudwatch-logs-commands)
- [Secrets Manager Commands](#secrets-manager-commands)
- [EC2 Hands-on Commands (Tech Tuesday)](#ec2-hands-on-commands-tech-tuesday)
- [References](#references)

</details>

---

## Initial Setup Commands

### Check CLI Version
```sh
aws --version
```

### List Profiles
```sh
aws configure list-profiles
```

### View Profile Configuration
```sh
aws configure list --profile <profile-name>
```

### Configure Profile
```sh
aws configure --profile <profile-name>
```

### AWS SSO Login
```sh
aws sso login --profile <profile-name>
export AWS_PROFILE=<profile-name>
```

---

## S3 Commands

### List Buckets
```sh
aws s3 ls
```
```sh
aws s3 ls --profile <profile-name>
```

### Create Bucket
```sh
aws s3 mb s3://<bucket-name>/
```
```sh
aws s3 mb s3://<bucket-name>/ --profile <profile-name>
```

### List Files Inside a Bucket
```sh
aws s3 ls s3://<bucket-name>/
```

### Upload a File
```sh
aws s3 cp <local-file> s3://<bucket-name>/<file>
```

### Download a File
```sh
aws s3 cp s3://<bucket-name>/<file> <local-file>
```

### Remove a File
```sh
aws s3 rm s3://<bucket-name>/<file>
```

### Delete Bucket
```sh
aws s3 rb s3://<bucket-name> --force
```

### Get Bucket Location
```sh
aws s3api get-bucket-location --bucket <bucket-name>
```

---

## Lambda Commands

### List Lambda Functions
```sh
aws lambda list-functions
```

### Create Lambda Function
```sh
aws lambda create-function   --function-name "MyFunction"   --runtime "nodejs18.x"   --role <iam-role-arn>   --handler "index.handler"   --zip-file "fileb://function.zip"
```

### Invoke Lambda Function
```sh
aws lambda invoke   --function-name "MyFunction"   --payload '{"key":"value"}'   output.txt
```

---

## API Gateway Commands
```sh
aws apigateway get-rest-apis
```

### Create REST API
```sh
aws apigateway create-rest-api --name "TestAPI"
```

### Deploy API
```sh
aws apigateway create-deployment   --rest-api-id <rest-api-id>   --stage-name "prod"
```

---

## Cognito Commands

### Create User Pool
```sh
aws cognito-idp create-user-pool --pool-name "MyUserPool"
```

### Create User Pool Client
```sh
aws cognito-idp create-user-pool-client   --user-pool-id <pool-id>   --client-name "MyClientApp"
```

---

## CloudFront Commands

### Create Distribution for Public S3
```sh
aws cloudfront create-distribution   --origin-domain-name <bucket>.s3.amazonaws.com   --default-root-object index.html
```

---

## CloudWatch Logs Commands

### Describe Log Groups
```sh
aws logs describe-log-groups
```

### Put Log Events
```sh
aws logs put-log-events   --log-group-name "log-group"   --log-stream-name "log-stream"   --log-events timestamp=12345,message="Hello World"
```

---

## Secrets Manager Commands

### Create Secret
```sh
aws secretsmanager create-secret   --name "MySecret"   --description "DB Password"   --secret-string '{"username":"admin","password":"MyP@ssw0rd"}'
```

### List Secrets
```sh
aws secretsmanager list-secrets
```

### Get Secret Value
```sh
aws secretsmanager get-secret-value   --secret-id MySecret
```

### Update Secret
```sh
aws secretsmanager update-secret   --secret-id MySecret   --secret-string '{"username":"admin","password":"NewP@ssw0rd"}'
```

### Delete Secret (Scheduled)
```sh
aws secretsmanager delete-secret   --secret-id MySecret   --recovery-window-in-days 7
```

---

## EC2 Hands-on Commands (Tech Tuesday)

```sh
chmod 400 "key.pem"
ssh -i "key.pem" ec2-user@<PUBLIC_IP>
sudo yum install httpd -y
sudo systemctl start httpd
cd /var/www/html
sudo bash -c 'echo "<h1>Hello AWS</h1>" > index.html'
sudo tail -f /var/log/httpd/access_log
```

---

## References
- AWS CLI S3 Docs  
- AWS CLI Secrets Manager Docs  

