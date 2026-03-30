# Task 1: Understand Infrastructure as Code
Before touching the terminal, research and write short notes on:

## What is Infrastructure as Code (IaC)? Why does it matter in DevOps?
IAC means deploying and managing infrastructure with code in a , instead of creating every server, network etc. manually. It helps deploying infrastucture reliably and past and that is why it is very importan in devops.

## What problems does IaC solve compared to manually creating resources in the AWS console?
When you use IAC, you can create infrastructure quickly and reliably.

## How is Terraform different from AWS CloudFormation, Ansible, and Pulumi?
AWS Cloudformation can oly be used with AWS while Terraform can be used with local, Azure, GCP etc as well.
Ansible is imperative in nature whild Terraform is delclarative.
Terrafoem works with HCL while pulumi can work with Python and Go.

## What does it mean that Terraform is "declarative" and "cloud-agnostic"?
Declarative means that in Terraform you just write down in once what you need and it teake cares on the creating that resource on its own as a command.
Clout-agnostic means that Terraform can be used across multiple cloud providers to create infrastructure.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Install Terraform and Configure AWS

## Install and configure the AWS CLI:
##  Verify AWS access:

<img width="413" height="145" alt="image" src="https://github.com/user-attachments/assets/c018c3b9-b6fc-4fa2-8c18-f5b86b04adf0" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Your First Terraform Config -- Create an S3 Bucket

## Go to the AWS S3 console and verify your bucket exists.
<img width="696" height="58" alt="image" src="https://github.com/user-attachments/assets/d6a8091d-fe2d-4928-817c-719f0196a894" />

## What did terraform init download? What does the .terraform/ directory contain?

Terraform init downloaded the latest version of hashicorp/aws v6.38.0.
.terraform/ directory contains the provider and related dependencies to run the configuration.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Add an EC2 Instance

## Go to the AWS EC2 console and verify your instance is running with the correct name tag.

<img width="1461" height="55" alt="image" src="https://github.com/user-attachments/assets/b34e708d-5deb-4165-9fa4-695c06952bfe" />

## How does Terraform know the S3 bucket already exists and only the EC2 instance needs to be created?

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Understand the State File

## Open terraform.tfstate in your editor -- read the JSON structure
## Run these commands and document what each returns:

1. terraform show
It shows the resource that terraform has created and the current state of the resource.

2. terraform state list
Shows the resource created by terraform and is currently tracking.

3. terraform state show aws_s3_bucket.my-bucket
Gives complete details of the s3 bucket created.

4. terraform state show aws_instance.my_ec2_instance
Gived complete detail of the ec2 instance created.


## What information does the state file store about each resource?
The state file stores all the detail and information about the infrastructure created.

## Why should you never manually edit the state file?
Manually editing the state file can cause corruption, infrastructure mismatch etc.

## Why should the state file not be committed to Git?
This file can expose sensitive data about the setup.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Modify, Plan, and Destroy

## Change the EC2 instance tag from "TerraWeek-Day1" to "TerraWeek-Modified" in your main.tf
## Run terraform plan and read the output carefully:
1. What do the ~, +, and - symbols mean?
~ update in-place
+ 
- Destroy
2. Is this an in-place update or a destroy-and-recreate?
This is an in-place update.

## Verify the tag changed in the AWS console
<img width="1488" height="77" alt="image" src="https://github.com/user-attachments/assets/a8ac7f61-7fb7-48df-8f76-15da18be5a3a" />

## Verify in the AWS console -- both the S3 bucket and EC2 instance should be gone
<img width="1509" height="64" alt="image" src="https://github.com/user-attachments/assets/850ce1b9-9889-478d-a329-f7bcdcf9ba45" />

S3 bucket was deleted as well.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

## EC2 instance apply
<img width="1181" height="192" alt="image" src="https://github.com/user-attachments/assets/e16258b8-e36b-4654-9de5-12be398eed89" />

## What each Terraform command does (init, plan, apply, destroy, show, state list)
init - it initiated terraform to download all the required resouce
plan - Shows what changes Terraform will make without applying them
apply - Create the infrastructure
destroy - Deletes all managed infrastructure
show - Displays the current state or execution plan in human-readable form
state list - Lists all resources tracked in the Terraform state file

## What the state file contains and why it matters
- It contains the mapping of the infrastructre created, its attributes and dependencies. It is the source of truth of the infrastucture created.




