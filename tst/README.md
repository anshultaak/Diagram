

In the Terraform module folder, we have six modules,ecrrepo,fargate,pipeline-backend,pipeline-frontend,pulse-rds and slack-notifications
* Ecrrepo:- Under the ECRRepo module, we have stored the code to make an ECR repo.
* Fargate :- Under the Fargate module, we have the code to create an ECS Fargate cluster, an Application Load Balancer, and a DNS record.
* Pipeline-backend :- Under the pipeline-backend module IT makes a backend deployment application code.
* Pipeline-frontend :- Under the pipeline-frontend module IT makes a FRONTend deployment application code....
* Pulse-rds:- Pulse-RDS makes MySQL RDS database backups.
* Slack-notification:- Slack notification module integrates code pipeline notification with DevOps notification channel under the Slack notification module.

* Ecrrepo:
Under the ECR repo, we create the Terraform TF files. Under those TF files, we create the ECR repo resoucre and IAM cross-account policies. These cross-region policies are created because ECR repository is on one AWS account and Ecs clusters are present on different AWS accounts for the communication between ECR and ECS, so we created cross-region policies.

* Fargate
Initially, a VPC is created in the us-west-2 region and within the VPC, two public and two private subnets are created in us-west-2a and us-west-2b availability zones. An ECS Fargate Cluster including containers are created under the Private subnet.

* Pulse-rds
Under the pulse-rds repo, we create the db.tf files. Under those db.tf files, we create the db subnet group, identifier and the  mysql engine, username, and password.

* Slack-notification
Under the Slack Notification repository, we create the Terraform TF files. Under those Terraform TF files, we create the Slack Notification resources, AWS IAM role, AWS Chatbot Slack channel guardrail policies, and AWS IAM role policies.
