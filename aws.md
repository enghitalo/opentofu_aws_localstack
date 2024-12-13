# AWS CLI

## Install and update

```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install --bin-dir /usr/local/bin --install-dir /usr/local/aws-cli --update
```

## First Run

```sh
aws configure
```

## Running with localstack

```sh
export AWS_ACCESS_KEY_ID=key
export AWS_SECRET_ACCESS_KEY=secret
export AWS_DEFAULT_REGION=us-east-1

# Creates an S3 bucket.
aws --endpoint-url="http://localhost:4566" s3 mb s3://my-bucket --region us-east-1
aws --endpoint-url="http://localhost:4566" s3 ls

# Upload a file to the S3 bucket.
aws --endpoint-url="http://localhost:4566" s3 cp aws.md s3://my-bucket/

# Remove a file from the S3 bucket.
aws --endpoint-url="http://localhost:4566" s3 rm s3://my-bucket/aws.md

# Delete all files and then the S3 bucket
aws --endpoint-url="http://localhost:4566" s3 rb s3://my-bucket --force
```
