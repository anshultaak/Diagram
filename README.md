# Diagram

![Untitled Diagram drawio (8)](https://user-images.githubusercontent.com/76546821/215265956-45f82a59-bfba-4714-84cf-798a4bef0830.png)


First, we need to create a GitHub repository and provide access to the repository and push the code into the repository.


We need to do one thing manually: log in to the AWS account where you need to deploy our application and create two secrets with the names "emrimages" and "github".

We need to create one ECR repository and push the images there. For ECR, we have one common AWS account for all projects with the name "Verb-common"; you can create an ECR repository by triggering this Terraform script.
