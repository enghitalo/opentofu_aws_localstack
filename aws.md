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

## Localstack profile

```sh
# Add AWS credentials to the .aws/credentials file
cat << END_OF_TEXT_TRANSMISSION >> ~/.aws/credentials

[localstack]
aws_access_key_id=key
aws_secret_access_key=secret
END_OF_TEXT_TRANSMISSION
```

```sh
# Add AWS profile config
cat << END_OF_TEXT_TRANSMISSION >> ~/.aws/config

[profile localstack]
region=us-east-1
endpoint_url=http://localhost:4566
END_OF_TEXT_TRANSMISSION
```

## Running with localstack

```sh
# Creates an S3 bucket.
aws --profile localstack s3 mb s3://my-bucket --region us-east-1
aws --profile localstack s3 ls

# Upload a file to the S3 bucket.
aws --profile localstack s3 cp aws.md s3://my-bucket/

# Download a file from the S3 bucket.
aws --profile localstack s3 cp s3://my-bucket/aws.md downloaded_aws.md

# Remove a file from the S3 bucket.
aws --profile localstack s3 rm s3://my-bucket/aws.md

# Delete all files and then the S3 bucket
aws --profile localstack s3 rb s3://my-bucket --force
```

or

```sh
export AWS_ACCESS_KEY_ID=key
export AWS_SECRET_ACCESS_KEY=secret
export AWS_DEFAULT_REGION=us-east-1

# Creates an S3 bucket.
aws --endpoint-url="http://localhost:4566" --region us-east-1 s3 mb s3://my-bucket --region us-east-1
aws --endpoint-url="http://localhost:4566" --region us-east-1 s3 ls

# Upload a file to the S3 bucket.
aws --endpoint-url="http://localhost:4566" --region us-east-1 s3 cp aws.md s3://my-bucket/

# Remove a file from the S3 bucket.
aws --endpoint-url="http://localhost:4566" --region us-east-1 s3 rm s3://my-bucket/aws.md

# Delete all files and then the S3 bucket
aws --endpoint-url="http://localhost:4566" --region us-east-1 s3 rb s3://my-bucket --force
```
