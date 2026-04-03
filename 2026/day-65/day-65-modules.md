# Task 1: Understand Module Structure

## What is the difference between a "root module" and a "child module"?
"root module" is the main working directory where you run terraform init, apply etc. 
"child module" is the directly which keeps the files being called root module files.

++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Build a Custom EC2 Module

## variables.tf

variable "ami_id" {
  type    = string
  description = "AMI ID for the EC2 instances"
}

variable "instance_type" {
  type    = string
  description = "EC2 instance type"
  default = "t2.micro"
}

variable "subnet_id" {
  type    = string
  description = "subnet id where instance will be launched"
}


variable "security_group_ids" {
  type        = list(string)
  description = "List of security group ids"
}

variable "instance_name" {
  type        = string
  description = "name tag for the instance"
}

variable "tags" {
  type        = map(string)
  description = "common tags for resource"
  default	  = {}
}


## main.tf
resource "aws_instance" "terraweek_ec2_instance_day65" {

  ami                    = var.ami_id
  instance_type          = var.instance_type
  subnet_id				= var.subnet_id
  vpc_security_group_ids	= var.security_group_ids

  root_block_device {
    volume_size = 10
    volume_type = "gp3"
  }

  tags = merge(var.tags, {
    Name = var.instance_name
  })
}


## Outputs.tf

output "instance_id" {
  description = "ID of ec2 instance"
  value       = aws_instance.terraweek_ec2_instance_day65.id
}

output "instance_public_ip" {
  description = "Public IP of ec2 instance"
  value       = aws_instance.terraweek_ec2_instance_day65.public_ip
}

output "instance_private_ip" {
  description = "Private IP address of the ec2 instance"
  value       = aws_instance.terraweek_ec2_instance_day65.private_ip
}

++++++++++++++++++++++++++++++++++++++++++++++++++++

## Task 4: Call Your Modules from Root

<img width="783" height="46" alt="image" src="https://github.com/user-attachments/assets/9adcf3c0-e064-48f7-a1be-69eb121d89d5" />












