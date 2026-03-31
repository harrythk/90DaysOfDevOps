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

# Task 4: Add a Security Group and EC2 Instance
Add to your config:

aws_security_group in the VPC:

Ingress rule: allow SSH (port 22) from 0.0.0.0/0
Ingress rule: allow HTTP (port 80) from 0.0.0.0/0
Egress rule: allow all outbound traffic
Tag: "TerraWeek-SG"
aws_instance in the subnet:

Use Amazon Linux 2 AMI for your region
Instance type: t2.micro
Associate the security group
Set associate_public_ip_address = true
Tag: "TerraWeek-Server"
Apply and verify -- your EC2 instance should have a public IP and be reachable.

<img width="639" height="116" alt="image" src="https://github.com/user-attachments/assets/b0e2567a-1a6e-41ab-be6e-7abab3fda7ce" />

<img width="755" height="38" alt="image" src="https://github.com/user-attachments/assets/6e303a52-a6eb-4c5d-9a3d-73186b761616" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: Explicit Dependencies with depends_on
Sometimes Terraform cannot detect a dependency automatically.

Add a second aws_s3_bucket resource for application logs
Add depends_on = [aws_instance.main] to the S3 bucket -- even though there is no direct reference, you want the bucket created only after the instance
## Run terraform plan and observe the order

<img width="916" height="395" alt="image" src="https://github.com/user-attachments/assets/4c4c2544-b5da-4009-a599-ddb095c50581" />

S3 bucket is created after EC2 instance as we have added depends_on.

## Now visualize the entire dependency tree:
terraform graph | dot -Tpng > graph.png

and paste the output into an online Graphviz viewer.

<img width="517" height="193" alt="image" src="https://github.com/user-attachments/assets/009fb3c0-eb58-4258-8846-0ad635f5ee4a" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Lifecycle Rules and Destroy
## Add a lifecycle block to your EC2 instance:
lifecycle {
  create_before_destroy = true
}
## Change the AMI ID to a different one and run terraform plan -- observe that Terraform plans to create the new instance before destroying the old one
Terraform plan to create and then destroy ec2 instance.
<img width="632" height="110" alt="image" src="https://github.com/user-attachments/assets/02b63175-1ee4-4577-8eb8-a19d1661322b" />

Destroy everything:
terraform destroy
## Watch the destroy order -- Terraform destroys in reverse dependency order. Verify in the AWS console that everything is cleaned up.

<img width="448" height="263" alt="image" src="https://github.com/user-attachments/assets/df0ba914-39ea-4912-9e51-0df1571550ba" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Main.tf

# Creating AWS VPC

resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"

  tags = {
    Name = "TerraWeek-VPC"
  }
}

# Creating AWS subnet

resource "aws_subnet" "main_subnet" {
  vpc_id                  = aws_vpc.main.id
  map_public_ip_on_launch = true
  cidr_block              = "10.0.1.0/24"

  tags = {
    Name = "TerraWeek-Public-Subnet"

  }
}

# Creating Internet Gateway

resource "aws_internet_gateway" "gw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "Terraweek_gateway"
  }
}

# Creating route table

resource "aws_route_table" "terraweek_route" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.gw.id
  }
}

# attaching route table and internet gateway

resource "aws_route_table_association" "terraweek_route_asso" {
  subnet_id      = aws_subnet.main_subnet.id
  route_table_id = aws_route_table.terraweek_route.id
}

# Creating ingress and egress

resource "aws_security_group" "allow_tls" {
  name        = "allow_tls"
  description = "Allow TLS inbound traffic and all outbound traffic"
  vpc_id      = aws_vpc.main.id

  tags = {
    Name = "Terraweek-security-group"
  }
}

resource "aws_vpc_security_group_ingress_rule" "allow_ssh" {
  security_group_id = aws_security_group.allow_tls.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 22
  ip_protocol       = "tcp"
  to_port           = 22
}

resource "aws_vpc_security_group_ingress_rule" "allow_http" {
  security_group_id = aws_security_group.allow_tls.id
  cidr_ipv4         = "0.0.0.0/0"
  from_port         = 80
  ip_protocol       = "tcp"
  to_port           = 80
}

resource "aws_vpc_security_group_egress_rule" "allow_all_traffic" {
  security_group_id = aws_security_group.allow_tls.id
  cidr_ipv4         = "0.0.0.0/0"
  ip_protocol       = "-1" # semantically equivalent to all ports
}

# Creating EC2 instance

resource "aws_instance" "terraweek_ec2_instance" {
  ami                         = "ami-0ec10929233384c7f" # us-east-1
  instance_type               = "t2.micro"
  subnet_id                   = aws_subnet.main_subnet.id
  vpc_security_group_ids      = [aws_security_group.allow_tls.id]
  associate_public_ip_address = "true"

  lifecycle {
  create_before_destroy = true
}
  tags = {
    Name = "TerraWeek-Server"
  }
}

resource "aws_s3_bucket" "my-second-bucket" {
  bucket     = "terraweek-second-bucket-2026"
  depends_on = [aws_instance.terraweek_ec2_instance]

  tags = {
    Name = "My second s3 bucket"
  }
}
