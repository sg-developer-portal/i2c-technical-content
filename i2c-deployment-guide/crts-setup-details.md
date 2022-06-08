## AWS Elastic Container Registry

### Create repository for CRTS

![Fig 1: Create repository for CRTS.](/assets/create-repository-for-crts.png)

### Take note of the Universal Resource Identifier (URI) after the repository creation

![Fig 2: Universal Resource Identifier (URI) after the repository creation.](/assets/universal-resource-identifier.png)

## Dockerfile

### Prerequisite

- Install AWS CLI
- Install Docker

Reference: [Using Amazon ECR with the AWS CLI](https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html ':target=_blank')

### Dockerfile for CRTS

1. Unzip the docker package zip file to local.

2. Open the Command Prompt cmd on the extracted directory and run docker build command.

   ```bash
   docker build -t crts
   ```

3. Run docker tag command to tag the image with the AWS ECR URI

   ```bash
   docker tag crts-aws:latest "331489159872.dkr.ecr.ap-southeast-1.amazonaws.com/crts":latest
   ```
   
   - *Replace the highlighted value with the URI from [here](/crts-setup-details?id=take-note-of-the-universal-resource-identifier-uri-after-the-repository-creation)*

4. Run docker push command to push the local image to AWS ECR.

   ```bash
   docker push 331489159872.dkr.ecr.ap-southeast-1.amazonaws.com/crts:latest
   ```

5. Verify the upload status from AWS ECR

![Fig 3: Verify the upload status from AWS ECR.](/assets/verify-status.png)

6. Take note of this image URI of latest tag because will use this as part of AWS Batch setup later.

![Fig 4: Image URI](/assets/copy-uri.png)

## AWS Batch

### Compute Environments

![Fig 5: Compute Environments](/assets/compute-environments.png)

### Job Queue

1. Create Job Queue for crts-aws (example name: crts-aws-jq).

![Fig 6: Create Job Queue.](/assets/job-queue.png)

2. Select the same compute environments created [here](/crts-setup-details?id=compute-environments).

![Fig 7: Select compute environments.](/assets/select-compute-environments.png)

### Job Definitions

1. Create Job Definition for AWS (example name: CrtsAwsJD).

![Fig 8: Create Job Definition for AWS.](/assets/create-job-definition.png)

2. Replace the Container properties with the ECR URI created [here](/crts-setup-details?id=dockerfile-for-crts) (for AWS).

![Fig 9: Replace the Container properties.](/assets/replace-container-properties.png)

3. Remember to enable “Assign public IP”.

![Fig 10: Enable "Assign public IP".](/assets/enable-assign-public-ip.png)

4. Create job definition with following settings.

![Fig 11: Create job definition with following settings.](/assets/job-definition-settings.png)

## AWS Lambda

### Lambda triggers the AWS Batch

1. Unzip the code for triggering the AWS Batch created in 5.3 AWS Batch.

2. Create AWS Lambda with Python 3.8 Runtime and paste the code into lambda_function.py .

3. Go to Configuration -> Environment Variables, add in

   - aws_jobdefinition
   - aws_jobqueue
   
   ```bash
   # Sample value
   CrtsAwsJD:2
   ```
   
   - Value of the environment variables can get from AWS Batch [Job Queue](/crts-setup-details?id=job-queue) and [Job Definitions](/crts-setup-details?id=job-definitions), note that the value of JD will need to include revision number (:2) if not revision 1.
   
4. Go to Configuration -> Permissions and add in actions below:

   - Allow: batch:SubmitJob

   ```bash
	Policy Value:
	{
		"Version": "2012-10-17",
		"Statement": [
			{
				"Sid": "VisualEditor0",
				"Effect": "Allow",
				"Action": "batch:SubmitJob",
				"Resource": "*"
			}
		]
	}
   ```

![Fig 12: Enable batch:SubmitJob.](/assets/permission-policies.png)

![Fig 13: Create policy in JSON.](/assets/json-code.png)

![Fig 14: Policies created.](/assets/policies-created.png)

5. With the lambda and API Gateway, there is the  ability to trigger the AWS Batch via the API.

## AWS API Gateway

### Creation via Lambda

1. Create an API Gateway using Lambda, go to the AWS Lambda created [here](/crts-setup-details?id=lambda-triggers-the-aws-batch).

2. Go to Lambda Configuration -> Triggers -> Add Trigger with settings below:

![Fig 15: Add Triggers in Lambda configuration.](/assets/add-triggers-in-lambda-configuration.png)

3. After the creation of API Gateway, click on Actions to “Create Method” and select "POST".

![Fig 16: Create POST method.](/assets/create-post-method.png)

4. Next is to configure the lambda integration, by putting the lambda function name to the textbox and check “Lambda Proxy Integration” below:

![Fig 17: Configure lambda integration.](/assets/configure-lambda-integration.png)

5. On Method Execution screen, click on “Method Request”:

![Fig 18: Select Method Request.](/assets/select-method-request.png)

6. On the Method Request, ensure API Key Required is set to **true**:

![Fig 19: Set API Key Required to true.](/assets/api-key-required.png)

7. Select the “ANY” method and run “Delete Method”. After deleted “ANY”, can proceed with next step.

![Fig 20: Run delete method.](/assets/run-delete-method.png)

8. To test out the API Gateway, will need to create API Keys and then either use Postman. The API key will  be appended in the request header x-api-key.

![Fig 21: Test API Gateway.](/assets/test-api-gateway.png)

9. Next is the configuration for CORS -> Enable CORS.

![Fig 22: Configuring the CORS.](/assets/configure-cors.png)

10. After enabled the CORS settings, go to POST method -> Method Response.

![Fig 23: POST method in CORS settings.](/assets/post-method-in-cors-settings.png)

11. On page Method Response, update the response Headers for 200 as shown below:

![Fig 24: Update response headers for 200.](/assets/update-response-header-for-200.png)

12. After done with all the configurations, select crts:

![Fig 25: Select CRTS in CORS configuration.](/assets/select-crts-in-cors-config.png)

   - Click on Deploy API:
   
![Fig 26: Click on Deploy API.](/assets/deploy-api.png)
   
   - Choose default:
   
![Fig 27: Choose default when deploying API.](/assets/choose-default.png)

13. CORS setting will need to verify using Swagger, on the steps listed [here](/crts-setup-details?id=access-the-crts-api-in-aws-api-gateway-using-swagger).

## Swagger via AWS S3

### AWS S3

1. Create a new S3 and allow public access:

![Fig 28: Create a new S3 and allow public access.](/assets/create-new-s3.png)

2. After S3 creation, go to bucket Properties and enable Static web hosting:

![Fig 29: Enable static web hosting.](/assets/enable-static-web-hosting.png)

3. Take note of the “Bucket website endpoint”, this will be used as URL to access swagger.

![Fig 29: Bucket website endpoint URL.](/assets/bucket-website-endpoint-url.png)

4. Go to Permissions -> Bucket Policy and put the value as below(replace the highlighted value to your S3 bucket name):

   ```bash
	{
		"Version": "2012-10-17",
		"Statement": [
			{
				"Sid": "PublicReadGetObject",
				"Effect": "Allow",
				"Principal": "*",
				"Action": "s3:GetObject",
				"Resource": "arn:aws:s3:::cris-swagger-bucket/*"
			}
		]
	}

   ```

5. Go to Permissions -> Cross-origin resource sharing (CORS) and put the value as below:

   ```bash
	[
		{
			"AllowedHeaders": [
				"*"
			],
			"AllowedMethods": [
				"PUT",
				"POST"
			],
			"AllowedOrigins": [
				"*"
			],
			"ExposeHeaders": []
		}
	]
   ```

### Swagger

1. Unzip the Swagger code and upload to the S3 bucket created [here](/crts-setup-details?id=aws-s3).
2. Need to update “crts-swagger.json” with the API gateway details (refer to [AWS API Gateway](/crts-setup-details?id=aws-api-gateway)), such as URL.
3. Upload the new configuration files to S3.
4. Should be able to browse the swagger website using the bucket website endpoint from [AWS S3](/crts-setup-details?id=aws-s3) step 3.

### Access the CRTS API in AWS API Gateway using Swagger

![Fig 30: CRTS job trigger API](/assets/crts-job-trigger-api.png)

![Fig 31: CRTS job trigger API parameters](/assets/crts-job-trigger-api-parameters.png)

![Fig 32: CRTS job trigger API body](/assets/crts-job-trigger-api-body.png)

![Fig 33: CRTS job trigger API success response](/assets/crts-job-trigger-api-success-response.png)
