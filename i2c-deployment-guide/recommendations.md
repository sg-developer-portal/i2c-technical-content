## Recommendations

1. Build Continuous Integration (CI)/Continuous Delivery (CD) pipeline for automation of Terraform Execution.
2. To improve the source code of process.sh and dockerfile, so that it can take in more than the 4 parameters below:
     - aws_access_key_id - AWS account ID.
	 - aws_secret_access_key - AWS account password.
	 - aws_s3reportbucket - storage destination.
	 - csp_resources (enhancement) – specify type of resource to be converted.
3. Copy generated code from S3 bucket and put into a Secure Internet Device and start modification without writing from the start.
4. To achieve end goal of 100% IaC for Infrastructure provisioning, all Human Accounts for the CSP portal should only grant “ReadOnly” Role, use IaC for any Add/Modify/Delete tasks. This is to avoid configuration drift.
5. To deploy I2C static URL frontend portal to run in internet isolated environment. This is to provide more flexibility and security when comes to I2C deployment.
6. To improve I2C to support newer version terraform executable and terraformer, so that I2C may potentially expand capabilities to support more features / recovering more CSP resources.
7. To use I2C as a tool to supplement CSP environment resource configuration backup. For existing and new implementation.
8. To improve I2C code base to be used for Azure CSP.
9. To improve I2C into an easily deployable infrastructure code so Agency can easily deploy the I2C on their CSP as required.
10. Using source code control system, to do versioning on the infrastructure code.
