# Task 1: Explore the AWS Provider

Create a new project directory: terraform-aws-infra
Write a providers.tf file:
Define the terraform block with required_providers pinning the AWS provider to version ~> 5.0
Define the provider "aws" block with your region
## Run terraform init and check the output -- what version was installed?
version 5.100.0 was installed.

<img width="1834" height="681" alt="image" src="https://github.com/user-attachments/assets/91fc2fe3-c4f4-4f77-9e7c-c245f2ace1f0" />

## Read the provider lock file .terraform.lock.hcl -- what does it do?
It contains the version of provider like aws that was downloaded during init.

## What does ~> 5.0 mean? How is it different from >= 5.0 and = 5.0.0?
~> 5.0 mean that version betwen 5.0 and 6.0 will be downloaded. Not 6.0 or above, same goes for 5.0 or below.
>= 5.0 mean that any version above 5.0 can be downloaded.
= 5.0.0 mean that version 5.0.0 will only be downloaded. 

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Build a VPC from Scratch
## Create a main.tf and define these resources one by one:
aws_vpc -- CIDR block 10.0.0.0/16, tag it "TerraWeek-VPC"
aws_subnet -- CIDR block 10.0.1.0/24, reference the VPC ID from step 1, enable public IP on launch, tag it "TerraWeek-Public-Subnet"
aws_internet_gateway -- attach it to the VPC
aws_route_table -- create it in the VPC, add a route for 0.0.0.0/0 pointing to the internet gateway
aws_route_table_association -- associate the route table with the subnet

<img width="1831" height="333" alt="image" src="https://github.com/user-attachments/assets/9da33713-7b9e-40a6-958a-b7add7196cc9" />

<img width="1669" height="711" alt="image" src="https://github.com/user-attachments/assets/5a502aa1-12d3-45b0-aa9e-75d3e19a78e5" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Understand Implicit Dependencies
Look at your main.tf carefully:

The subnet references aws_vpc.main.id -- this is an implicit dependency
The internet gateway references the VPC ID -- another implicit dependency
The route table association references both the route table and the subnet
Answer these questions:

## How does Terraform know to create the VPC before the subnet?
Subnet depends upon VPC that is why Terraform creates VPC before subnet.

## What would happen if you tried to create the subnet before the VPC existed?
If we try to create subnet before VPC, it will fail.

## Find all implicit dependencies in your config and list them
Subnet and Internet Gateway depends upon VPC. 
While Route table depends upon VPC and Internet gatway. 
Aoute table association depends upon Subnet and Route Table.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++




