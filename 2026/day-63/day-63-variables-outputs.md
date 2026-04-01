# Task 1: Extract Variables

<img width="917" height="299" alt="image" src="https://github.com/user-attachments/assets/5e6da28c-de17-4da1-93b3-3e4d4f7e7bfc" />


<img width="914" height="249" alt="image" src="https://github.com/user-attachments/assets/03d0f3fa-3691-44c2-9cb7-a11c11e47bf1" />

++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Variable Files and Precedence

## Apply with the default file:
It used the file terraform.tfvars

<img width="929" height="230" alt="image" src="https://github.com/user-attachments/assets/194281d6-e9f6-46bf-a5c2-8bb3bd77ed6f" />

## Apply with the prod file:
terraform plan -var-file="prod.tfvars" 

<img width="923" height="181" alt="image" src="https://github.com/user-attachments/assets/26581a4a-6a0e-4d90-9a3a-b361d148d855" />

<img width="569" height="119" alt="image" src="https://github.com/user-attachments/assets/bf94ada5-56ff-4196-b151-20c561afa778" />

## Override with CLI:
terraform plan -var="instance_type=t2.nano"

<img width="914" height="424" alt="image" src="https://github.com/user-attachments/assets/b05c7d0e-1630-4ecd-99d5-8ca9fe3be6f6" />

## Set an environment variable:
export TF_VAR_environment="staging"
terraform plan   

<img width="925" height="151" alt="image" src="https://github.com/user-attachments/assets/3dc69d3f-e16f-402d-ac84-2bea06a25ead" />

++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Add Outputs
Create an outputs.tf file with outputs for:

## terraform apply

<img width="1464" height="303" alt="image" src="https://github.com/user-attachments/assets/976bb00e-837b-4e7c-bfc7-6dfb68ed76ef" />

## terraform output
<img width="952" height="205" alt="image" src="https://github.com/user-attachments/assets/ea82023b-adbc-405d-9f1a-9b06fd9c1f95" />

## terraform output instance_public_ip 
<img width="1192" height="70" alt="image" src="https://github.com/user-attachments/assets/96a04f6a-f1c5-4459-aa2d-ea4837612e09" />

## terraform output -json 
<img width="659" height="638" alt="image" src="https://github.com/user-attachments/assets/348550e2-a1c4-4da4-beb8-2d92146165bb" />

++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Use Data Sources
Stop hardcoding the AMI ID. Use a data source to fetch it dynamically.

## Add a data "aws_ami" block that:

Filters for Amazon Linux 2 images
Filters for hvm virtualization and gp2 root device
Uses owners = ["amazon"]
Sets most_recent = true
## Replace the hardcoded AMI in your aws_instance with data.aws_ami.amazon_linux.id

## Add a data "aws_availability_zones" block to fetch available AZs in your region

## Use the first AZ in your subnet: data.aws_availability_zones.available.names[0]

<img width="667" height="608" alt="image" src="https://github.com/user-attachments/assets/c189ce34-d1fd-42a8-82da-81f47ca8be8b" />

<img width="1059" height="444" alt="image" src="https://github.com/user-attachments/assets/d62df606-2e3d-4748-9e39-4562c538d761" />

<img width="1083" height="379" alt="image" src="https://github.com/user-attachments/assets/a17a843e-3e19-4156-8a64-3979931a2a5a" />


<img width="1361" height="350" alt="image" src="https://github.com/user-attachments/assets/6c634514-1abf-4743-a778-1fc93a5f10ac" />

## What is the difference between a resource and a data source?
Resource - Create and destroy infrastructure
Data Source - Reads / fetch the available information

++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Use Locals for Dynamic Values

<img width="1019" height="449" alt="image" src="https://github.com/user-attachments/assets/ce0d5249-5597-4850-9669-2535c45e3932" />

<img width="1150" height="444" alt="image" src="https://github.com/user-attachments/assets/4110ef6d-38ee-425f-bfb7-a74955ff4c06" />

<img width="1212" height="449" alt="image" src="https://github.com/user-attachments/assets/7bd2fe16-0c20-4949-869a-1144c0aa33ea" />

++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Built-in Functions and Conditional Expressions

<img width="817" height="510" alt="image" src="https://github.com/user-attachments/assets/c4948765-143b-4538-a184-62b52d15006d" />

Conditional expression -- add this to your config:

instance_type = var.environment == "prod" ? "t3.small" : "t2.micro"
# Apply with environment = "prod" and verify the instance type changes.
<img width="635" height="226" alt="image" src="https://github.com/user-attachments/assets/3c589f3c-959c-4e24-a3a3-ef1b41f5261b" />
