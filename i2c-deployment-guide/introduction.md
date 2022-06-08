## Purpose

This deployment guide is developed based on outcomes of GovTech’s Capability Centre for Government ICT infrastructure (CapCEN) Proof of Concept (POC) for Cloud Resource Transformation Solution (CRTS) that was targeted for Amazon Web Services (AWS) in Government on Commercial  Cloud (GCC)1.0. It consists of detailed resources required, tools utilized and steps necessary for deployment of this solution into agencies’ AWS environment in GCC1.0.

## Audience

The intended audience are:

1. Infrastructure Engineers
2. DevOps Engineers

## Terms and Acronyms

<details>
 <summary>Amazon ECR</summary>
 <p>Amazon Elastic Container Registry (Amazon ECR) is an Amazon Web Services (AWS) managed container image registry service that is secure, scalable, and reliable. Amazon ECR supports private repositories with resource-based permissions using AWS IAM.</p>
</details>
 
<details> 
 <summary>Amazon Elastic Container Service (ECS)</summary>
 <p>Amazon Elastic Container Service (ECS) is a cloud computing service in Amazon Web Services (AWS) that manages containers and allows developers to run applications in the cloud without having to configure an environment for the code to run in.</p>
</details>
 
<details>  
 <summary>API</summary>
 <p>Application Programming Interface</p>
</details>
 
<details>  
 <summary>Amazon S3</summary>
 <p>Amazon S3 or Amazon Simple Storage Service is a service offered by Amazon Web Services (AWS) that provides object storage through a web service interface. Amazon S3 uses the same scalable storage infrastructure that Amazon.com uses to run its global e-commerce network. Amazon S3 can be employed to store any type of object, which allows for uses like storage for Internet applications, backup and recovery, disaster recovery, data archives, etc.</p>
</details>
 
<details>  
 <summary>AWS</summary>
 <p>Amazon Web Services</p>
</details>
 
<details>  
 <summary>AWS API Gateway</summary>
 <p>Amazon Web Services API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. APIs act as the "front door" for applications to access data, business logic, or functionality from backend services. Using API Gateway, RESTful APIs and WebSocket APIs can be created that enable real-time two-way communication applications. API Gateway supports containerized and serverless workloads, as well as web applications.</p>
</details>
 
<details>  
 <summary>AWS Batch</summary>
 <p>AWS Batch helps to run batch computing workloads on the AWS Cloud. Batch computing is a common way for developers, scientists, and engineers to access large amounts of compute resources. AWS Batch removes the undifferentiated heavy lifting of configuring and managing the required infrastructure, similar to traditional batch computing software. This service can efficiently provision resources in response to jobs submitted in order to eliminate capacity constraints, reduce compute costs, and deliver results quickly.</p>
</details>
 
<details>  
 <summary>AWS Fargate</summary>
 <p>AWS Fargate is a serverless compute engine for containers that works with both Amazon Elastic Container Service (ECS) and Amazon Elastic Kubernetes Service (EKS). Fargate makes it easy to focus on building applications.</p>
</details>
 
<details>  
 <summary>AWS IAM</summary>
 <p>AWS Identity and Access Management (IAM) provides fine-grained access control across all of AWS. With IAM, the administrator can specify who can access which services and resources, and under which conditions. With IAM policies, the administrator manages permissions to the workforce and systems to ensure least-privilege permissions.</p>
</details>
 
<details>  
 <summary>AWS Lambda</summary>
 <p>Amazon Web Services Lambda is an event-driven, serverless computing platform provided by Amazon as a part of Amazon Web Services. It is a computing service that runs code in response to events and automatically manages the computing resources required by that code.</p>
</details>
 
<details>  
 <summary>CapCEN</summary>
 <p>The Capability Centre for Government ICT infrastructure is to strengthen GovTech capabilities in architecting and designing secure, resilient and cost effective public sector's ICT infrastructure covering data centres, networks, platforms, end-points and system operations. The centre will spearhead assessment and applicability of new technologies in these domains and develop compelling use cases to encourage adoption, and also to develop technical competency within GovTech.</p>
</details>
 
<details> 
 <summary>Checkov</summary>
 <p>Checkov scans cloud infrastructure configurations to find misconfigurations before they're deployed.</p>
 <p>Checkov uses a common command line interface to manage and analyse infrastructure as code (IaC) scan results across platforms.</p>
</details>
 
<details>  
 <summary>CI/CD</summary>
 <p>CI/CD is an automation pipeline, CI means “Continuous Integration” and CD means “Continuous Delivery”.</p>
</details>
 
<details>  
 <summary>CLI</summary>
 <p>Command Line Interface program that accepts operating systems commands via text input to execute operating system functions.</p>
</details>

<details>  
 <summary>CMD</summary>
 <p>CMD is an acronym for Command. Command prompt, or CMD, is the command-line interpreter of Windows operating systems.</p>
</details>
 
<details>  
 <summary>Container</summary>
 <p>Containers are abstract units of software that have everything needed to run a workload or process.</p>
</details>
 
<details> 
 <summary>Docker</summary>
 <p>Docker is a set of platform-as-a-service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. The service has both free and premium tiers. The software that hosts the containers is called Docker Engine. It was first started in 2013 and is developed by Docker, Inc.</p>
</details>
 
<details>  
 <summary>driftctl</summary>
 <p>Infrastructure drift is a blind spot and a source of potential security issues.</p>
 <p>driftctl is a free and open-source CLI that warns of infrastructure drift and fills in the missing piece in your DevSecOps toolbox.</p>
</details>
 
<details> 
 <summary>I2C</summary>
 <p>Infra to Code.</p>
</details>
 
<details>  
 <summary>IaC</summary>
 <p>Infrastructure as code (IaC) is the process of managing and provisioning computer data centres through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.[1] The IT infrastructure managed by this process comprises both physical equipment, such as bare-metal servers, as well as virtual machines, and associated configuration resources. The definitions may be in a version control system. The code in the definition files may use either scripts or declarative definitions, rather than maintaining the code through manual processes, but IaC more often employs declarative approaches.</p>
</details>
 
<details>  
 <summary>JSON</summary>
 <p>JSON (JavaScript Object Notation) is an open standard file format and data interchange format that uses human-readable text to store and transmit data objects consisting of attribute–value pairs and arrays (or other serializable values). It is a common data format with diverse uses in electronic data interchange, including that of web applications with servers.</p>
</details>
 
<details> 
 <summary>Kubernetes</summary>
  <p>Kubernetes defines a set of building blocks ("primitives"), which collectively provide mechanisms that deploy, maintain, and scale applications based on CPU, memory or custom metrics. Kubernetes is loosely coupled and extensible to meet different workloads.</p>
</details>
 
<details>  
 <summary>POC</summary>
 <p>Proof of Concept.</p>
</details>
 
<details> 
 <summary>Postman</summary>
 <p>Postman is an application used for API testing. It is an HTTP client that tests HTTP requests, utilizing a graphical user interface, through which to  obtain different types of responses that need to be subsequently validated. When it comes to REST APIs, use Postman as a GUI (graphical user interface).</p>
</details>
 
<details>  
 <summary>Restful API</summary>
 <p>Designed to take advantage of existing protocols. While REST - or Representational State Transfer - can be used over nearly any protocol, when used for web APIs it typically takes advantage of HTTP. This means that developers have no need to install additional software or libraries when creating a REST API.</p>
 <p>One of the key advantages of REST APIs is that they provide a great deal of flexibility. Data is not tied to resources or methods, so REST can handle multiple types of calls, return different data formats and even change structurally with the correct implementation of hypermedia. This flexibility allows developers to build an API that meets the needs of very diverse customers.</p>
</details>
 
<details>
 <summary>Serverless</summary>
 <p>Serverless offloads all management responsibility for backend cloud infrastructure and operations tasks - provisioning, scheduling, scaling, patching and more - to the cloud provider. This gives developers more time to develop and optimize their front-end application code and business logic. And with serverless, customers never pay for idle capacity. They pay only for the resources required to run their applications, and only when those applications are running. The name notwithstanding, there are most definitely servers in serverless computing. The term 'serverless' describes the customer's experience with those servers: they are invisible to the customer, who doesn't see them, manage them, or interact with them in any way.</p>
</details>
 
<details>
 <summary>Swagger UI</summary>
 <p>Swagger UI allows anyone — be it the development team or the end consumers — to visualize and interact with the API’s resources without having any of the implementation logic in place. It’s automatically generated from the OpenAPI (formerly known as Swagger) Specification, with the visual documentation making it easy for back end implementation and client side consumption.</p>
</details>
 
<details>  
 <summary>Terraform</summary>
 <p>Terraform is an open-source infrastructure as code software tool created by HashiCorp. Users define and provide data centre infrastructure using a declarative configuration language known as HashiCorp Configuration Language (HCL), or optionally JSON.</p>
</details>
 
<details>  
 <summary>Terraformer</summary>
 <p>A CLI tool that generates tf/json and tfstate files based on existing infrastructure (reverse Terraform).</p>
</details>
 
<details>
 <summary>tf</summary>
 <p>Terraform format configuration files.</p>
</details>
 
<details> 
 <summary>tfstate</summary>
 <p>Terraform must store state about managed infrastructure and configuration. This state is used by Terraform to map real world resources to the configuration, keep track of metadata, and to improve performance for large infrastructures.</p>
 <p>This state is stored by default in a local file named "terraform.tfstate", but it can also be stored remotely, which works better in a team environment.</p>
 <p>Terraform uses this local state to create plans and make changes to the  infrastructure. Prior to any operation, Terraform does a refresh to update the state with the real infrastructure.</p>
</details>
 
<details>
 <summary>URI</summary>
 <p>A Uniform Resource Identifier (URI) is a unique sequence of characters that identifies a logical or physical resource used by web technologies. URIs may be used to identify anything, including real-world objects, such as people and places, concepts, or information resources such as web pages and books. Some URIs provide a means of locating and retrieving information resources on a network (either on the Internet or on another private network, such as a computer filesystem or an Intranet); these are Uniform Resource Locators (URLs). A URL provides the location of the resource. A URI identifies the resource by name at the specified location or URL. Other URIs provide only a unique name, without a means of locating or retrieving the resource or information about it, these are Uniform Resource Names (URNs).</p>
</details>

<details>
 <summary>WebSocket API</summary>
 <p>The WebSocket API is an advanced technology that makes it possible to open a two-way interactive communication session between the user's browser and a server. With this API, you can send messages to a server and receive event-driven responses without having to poll the server for a reply.</p>
</details>