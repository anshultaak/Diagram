# Diagram

![Untitled Diagram drawio (8)](https://user-images.githubusercontent.com/76546821/215265956-45f82a59-bfba-4714-84cf-798a4bef0830.png)


First, we need to create a GitHub repository and provide access to the Devlopers and push the code into the repository.


We need to do one thing manually: log in to the AWS account where you need to deploy our application and create two secrets with the names "emrimages" and "github".

We need to create one ECR repository and push the images there. For ECR, we have one common AWS account for all projects with the name "Verb-common"; you can create an ECR repository by triggering this Terraform script.

Firstly, a VPC is created in the us-west-1 region and within the VPC, two public and two private subnets are created in us-west-1a and us-west-1b availability zones. An ECS Fargate Cluster is created and containers under the Private subnet 









How to access the application on the internet.
There are two containers available in private subnet.
Containers are connected with each other through an application load balancer.To access the application from outside.
The application load balancer is also interconnected with the security group and AWS Certificate Manager.
The security group is connected to an application load balancer used for security purposes.
In the security groups, we can define which traffic can access our application.
ACM are also connected with Application Load Balancers for managing AWS Certificates. ACM is designed to protect and manage the private keys used with SSL/TLS certificates.
Amazon Route 53 is a highly available and scalable Domain Name System (DNS) web service it returns IP addresses for dns records quired by the dns resolver.
 Route 53 connects user requests to internet applications running on AWS or on-premises.
 
 
First, we need to go to the GitHub repository where our code is available, and there we need to create a new folder named "build". Inside this folder, we need to create a code pipeline YAML file and a bash script.
For example, you can go with this link of Headless CMS application.

For the trigger pipeline, we need to create one release example "backend .0.0.1_dev1" and under the Code Pipeline use the S3 bucket to store our code and Secret Manager for image tag. Then push the image to the ECR repo which is present in the  verb-common AWS account After that, trigger the code build and code deploy, and it will deploy the application in containers.
