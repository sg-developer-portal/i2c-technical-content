The list of software tools utilised in this POC is shown below:

## Software Tools

1. **[Terraformer (ver 0.8.13)](https://github.com/GoogleCloudPlatform/terraformer ':target=_blank'):** The main Command Line Interface (CLI) tools used by CRTS solution to import cloud infrastructure.
2. **[Terraform (ver 0.12.31)](https://www.terraform.io/ ':target=_blank'):** Open-source infrastructure as code (IaC) software tools.
3. **[Checkov (ver 2.0.475)](https://www.checkov.io/ ':target=_blank'):** Scans cloud infrastructure provisioned and detects security and compliance misconfigurations using graph-based scanning.
4. **[Driftctl (ver 0.15.0)](https://driftctl.com/ ':target=_blank'):** Open-source CLI that warns of infrastructure drift.
5. **[Swagger-ui (swagger-ui-4.0.0-rc.2)](https://github.com/swagger-api/swagger-ui ':target=_blank'):** Allow to visualize and interact with the API’s resources without having any of the implementation logic in place.
6. **[Docker (ubuntu:20.04)](https://www.docker.com/ ':target=_blank'):** Open-source containerization platform.

## AWS Resources

Cloud resources utilised are as shown below:

1. **AWS Elastic Container Registry:** Using to host the dockerfile of CRTS solution.
2. **AWS Fargate:** Using to run the docker application of CRTS solution
3. **AWS Batch:** Using to schedule and trigger the AWS fargate to execute the CRTS solution
4. **AWS Lambda:** Using as the AWS Batch Trigger when receiving API request from API gateway
5. **AWS S3:** Using to upload the generated output. Hosting swagger static websites
6. **AWS API Gateway:** Allowing user to consume the CRTS API with api-key

