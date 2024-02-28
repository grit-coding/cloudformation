
# Create Nested S3 Buckets using AWS CloudFormation via AWS CLI

This guide outlines the process of creating a CloudFormation nested stack to generate two S3 buckets using AWS CLI and CloudFormation.

## Prerequisites
- AWS CLI installed on your machine.
- Proper AWS credentials configured with the necessary permissions.

## Configuration
First, configure your AWS credentials by setting the following environment variables:

```bash
export AWS_ACCESS_KEY_ID=yourAccessKey
export AWS_SECRET_ACCESS_KEY=YourSecretKey
export AWS_DEFAULT_REGION=us-east-1
```

## Steps

1. **Create a Bucket for Your Template**

   Create a new S3 bucket to store your CloudFormation template. Replace `gritcoding-bucketA` with your desired bucket name. Execute the following command:

   ```bash
   aws s3 mb s3://gritcoding-bucketA --region us-east-1 
   # Note: This will fail if the bucket name is not unique.
   ```

2. **Build the CloudFormation Template**

   Change your working directory to where your `main.json` file is located (assumed to be `create-two-nested-buckets`):

   ```bash
   cd create-two-nested-buckets
   ```

   Package your CloudFormation template with the following command:

   ```bash
   aws --region us-east-1 cloudformation package --s3-bucket gritcoding-bucketA --template-file ./main.json --output-template-file ./packaged-template.json --use-json
   ```

3. **Create a CloudFormation Stack**

  ```bash
  aws cloudformation deploy --template-file ./packaged-template.json --stack-name <your stack name>
  ```

4. ** Delete a CloudFormation Stack**

  ```bash
  aws cloudformation delete-stack --stack-name <your stack name>
  ```

## Additional Information

The main purpose of this guide is to demonstrate the creation of a CloudFormation nested stack, which in turn will create two S3 buckets. For more detailed information, you may refer to a related blog post or additional AWS documentation.
