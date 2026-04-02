# Task 1: Inspect Your Current State

## How many resources does Terraform track?
Terraform tracks 13 resource

<img width="507" height="202" alt="image" src="https://github.com/user-attachments/assets/62686386-e788-4d16-a942-1aa79ab8fb0a" />

## What attributes does the state store for an EC2 instance? (hint: way more than what you defined)
It store lot of attributes like arn, ami, id, availability zone etc.

<img width="777" height="469" alt="image" src="https://github.com/user-attachments/assets/6c798d7f-4d99-4790-b7f2-681760296fdd" />

## Open terraform.tfstate in an editor -- find the serial number. What does it represent?
It is a version of a state file.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 2: Set Up S3 Remote Backend

## Check the S3 bucket -- you should see dev/terraform.tfstate
<img width="687" height="36" alt="image" src="https://github.com/user-attachments/assets/10dca4cd-e07e-4ce3-963c-1b35bc271047" />

## Your local terraform.tfstate should now be empty or gone
It is empty

## Run terraform plan -- it should show no changes (state migrated correctly)
<img width="712" height="282" alt="image" src="https://github.com/user-attachments/assets/51b1beac-0e64-4f17-ad6a-b713ef8fe46b" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 3: Test State Locking

## What is the error message? Why is locking critical for team environments?
Terraform locked the state to protect the state from being written by multiple users at the same time.
<img width="548" height="205" alt="image" src="https://github.com/user-attachments/assets/e4b3d343-5de9-4b64-90e1-733d6bee89a1" />


+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 4: Import an Existing Resource

## terraform import aws_s3_bucket.imported terraweek-import-test-<yourname>

<img width="908" height="331" alt="image" src="https://github.com/user-attachments/assets/82a6d908-ff05-43b5-9871-5cb35f461f9d" />

## terraform plan
<img width="902" height="329" alt="image" src="https://github.com/user-attachments/assets/17a68e4b-fe2d-402a-bd79-719cc9d3d16a" />

## Run terraform state list -- the imported bucket should now appear alongside your other resources
<img width="499" height="223" alt="image" src="https://github.com/user-attachments/assets/94d3a22a-2f60-48f0-9003-a637cea41874" />

## What is the difference between terraform import and creating a resource from scratch?
Terraform import just imports the resource already created in AWS and starts managing it. While creating a new resource with terrafrom created the new resource and then manages it.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 5: State Surgery -- mv and rm

## Rename a resource in state:
terraform state list                              
terraform state mv aws_s3_bucket.imported aws_s3_bucket.logs_bucket
<img width="815" height="76" alt="image" src="https://github.com/user-attachments/assets/4d5b9014-28a2-4c84-9303-a98fc3c0ac95" />

## Remove a resource from state (without destroying it):
terraform state rm aws_s3_bucket.logs_bucket
<img width="667" height="77" alt="image" src="https://github.com/user-attachments/assets/cc3132ba-4e87-4566-8572-0793342f0270" />

## Re-import it to bring it back:
terraform import aws_s3_bucket.logs_bucket terraweek-import-test-<yourname>
<img width="1839" height="617" alt="image" src="https://github.com/user-attachments/assets/32d389f2-2669-4aed-a980-3a526768c464" />

## When would you use state mv in a real project? When would you use state rm?
state mv is used when you need to reorganize resource whithout creating a new one.
state rm is used when you does want taerraform to further manage a resource. 

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

# Task 6: Simulate and Fix State Drift

Apply your full config so everything is in sync
Go to the AWS console and manually:
Change the Name tag of your EC2 instance to "ManuallyChanged"
Change the instance type if it's stopped (or add a new tag)
Run:
terraform plan
## You should see a diff -- Terraform detects that reality no longer matches the desired state.

<img width="1826" height="750" alt="image" src="https://github.com/user-attachments/assets/d98bfb40-23aa-497e-ade5-5315317d991a" />

<img width="1851" height="647" alt="image" src="https://github.com/user-attachments/assets/994e30fd-b8fe-42c7-b941-4454ebecf664" />

## terraform apply
Name and instance type restored.

<img width="823" height="20" alt="image" src="https://github.com/user-attachments/assets/675e541d-cb47-43fc-8ee4-6865a5c43ef4" />

## terraform plan

<img width="720" height="292" alt="image" src="https://github.com/user-attachments/assets/1bcf8f1e-a721-4aeb-aecb-b1c356df3b42" />

## How do teams prevent state drift in production? (hint: restrict console access, use CI/CD for all changes)
Teams prevent state drift by restricting direct changes in the cloud console (using IAM policies) and ensuring all infrastructure changes go through Terraform via CI/CD pipelines.
This enforces a single source of truth (code) and keeps the actual infrastructure consistent with the Terraform state.

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++

Remote state digram:
<img width="186" height="174" alt="image" src="https://github.com/user-attachments/assets/1e9cf629-a0e7-41de-8a63-06202f169bfd" />

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++



