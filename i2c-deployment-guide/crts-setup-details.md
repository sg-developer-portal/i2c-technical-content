## AWS Elastic Container Registry

#### Create repository for CRTS

![Fig 1: Create repository for CRTS](/assets/create-repository-for-crts.png)

#### Take note of the Universal Resource Identifier (URI) after the repository creation

![Fig 2: Universal Resource Identifier (URI) after the repository creation](/assets/universal-resource-identifier.png)

## Dockerfile

#### Prerequisite

- Install AWS CLI
- Install Docker

Refernce: [Using Amazon ECR with the AWS CLI](https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html ':target=_blank')

#### Dockerfile for CRTS

1. Unzip the docker package zip file to local.

2. Open the Command Prompt cmd on the extracted directory and run docker build command.

   ```bash
   docker build -t crts
   ```

3. Run docker tag command to tag the image with the AWS ECR URI

   ```bash
   docker tag crts-aws:latest "331489159872.dkr.ecr.ap-southeast-1.amazonaws.com/crts":latest
   ```
   
*Replace the highlighted value with the URI from [here](/crts-setup-details?id=take-note-of-the-universal-resource-identifier-uri-after-the-repository-creation)*

4. Run docker push command to push the local image to AWS ECR.

   ```bash
   docker push 331489159872.dkr.ecr.ap-southeast-1.amazonaws.com/crts:latest
   ```

5. Verify the upload status from AWS ECR

![Fig 3: Verify the upload status from AWS ECR](/assets/verify-status.png)

6. Take note of this image URI of latest tag because will use this as part of AWS Batch setup later.

![Fig 4: Image URI](/assets/copy-uri.png)

## AWS Batch

**Compute Environments**

![Fig 5: Compute Environments](/assets/i2c-architecture.png)

**Job Queue**

![Fig 6: Job Queue](/assets/i2c-architecture.png)

**Job Definitions**

![Fig 7: Job Definitions](/assets/i2c-architecture.png)

## AWS Lambda

**Lambda triggers the AWS Batch**

![Fig 8: Lambda triggers the AWS Batch](/assets/i2c-architecture.png)

## AWS API Gateway

**Creation via Lambda**

![Fig 9: Creation via Lambda](/assets/i2c-architecture.png)

## Swagger via AWS S3

**AWS S3**

![Fig 10: AWS S3](/assets/i2c-architecture.png)

**Swagger**

![Fig 11: Swagger](/assets/i2c-architecture.png)

**Access the CRTS API in AWS API Gateway using Swagger**

![Fig 12: Access the CRTS API in AWS API Gateway using Swagger](/assets/i2c-architecture.png)