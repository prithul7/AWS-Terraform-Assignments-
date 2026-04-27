1. Install vs code
Install terraform cli
Configure aws cli
Deploy an ec2 instance using Terraform
Commands :
terraform init
terraform plan
terraform apply

ans:

![image.png](attachment:31e8a0c2-3f07-465d-910c-af12c01fae4e:image.png)

![image.png](attachment:067b3631-2ff4-4073-9f96-702abdcedbab:image.png)



2. Create a Terraform code for:
VPC
Public + Private subnets
Internet Gateway
NAT Gateway
Route tables
use remote state backend for this

ans: Main.tf

resource "aws_vpc" "main" {
cidr_block = "10.0.0.0/16"

tags = {
Name = "MyVPC"
}
}

resource "aws_subnet" "public" {
vpc_id                  = aws_vpc.main.id
cidr_block              = "10.0.1.0/24"
map_public_ip_on_launch = true

tags = {
Name = "Public-Subnet"
}
}

resource "aws_subnet" "private" {
vpc_id     = aws_vpc.main.id
cidr_block = "10.0.2.0/24"

tags = {
Name = "Private-Subnet"
}
}

resource "aws_internet_gateway" "igw" {
vpc_id = aws_vpc.main.id

tags = {
Name = "IGW"
}
}

resource "aws_eip" "nat_eip" {
domain = "vpc"
}

resource "aws_nat_gateway" "nat" {
allocation_id = aws_eip.nat_eip.id
subnet_id     = aws_subnet.public.id

tags = {
Name = "NAT-Gateway"
}
}

resource "aws_route_table" "public_rt" {
vpc_id = aws_vpc.main.id
}

resource "aws_route" "public_internet" {
route_table_id         = aws_route_table.public_rt.id
destination_cidr_block = "0.0.0.0/0"
gateway_id             = aws_internet_gateway.igw.id
}

resource "aws_route_table_association" "public_assoc" {
subnet_id      = aws_subnet.public.id
route_table_id = aws_route_table.public_rt.id
}

resource "aws_route_table" "private_rt" {
vpc_id = aws_vpc.main.id
}

resource "aws_route" "private_nat" {
route_table_id         = aws_route_table.private_rt.id
destination_cidr_block = "0.0.0.0/0"
nat_gateway_id         = aws_nat_gateway.nat.id
}

resource "aws_route_table_association" "private_assoc" {
subnet_id      = aws_subnet.private.id
route_table_id = aws_route_table.private_rt.id
}

![image.png](attachment:b18c5ffa-511e-4c48-bd61-5cb57db85345:image.png)



3. Create a Terraform code for:
VPC
Public + Private subnets
Internet Gateway
NAT Gateway
Route tables
use remote state backend for this
Create public private ec2 instance in respective subnet as well

ans: main.tf

resource "aws_security_group" "ec2_sg" {
name        = "ec2-sg"
description = "Allow SSH"
vpc_id      = aws_vpc.main.id

ingress {
from_port   = 22
to_port     = 22
protocol    = "tcp"
cidr_blocks = ["0.0.0.0/0"]

}

egress {
from_port   = 0
to_port     = 0
protocol    = "-1"
cidr_blocks = ["0.0.0.0/0"]
}
}

resource "aws_instance" "public_ec2" {
ami                         = "ami-0ec10929233384c7f"
instance_type               = "t2.micro"
subnet_id                   = aws_subnet.public.id
vpc_security_group_ids      = [aws_security_group.ec2_sg.id]
associate_public_ip_address = true

tags = {
Name = "Public-EC2"
}
}

resource "aws_instance" "private_ec2" {
ami                    = "ami-0ec10929233384c7f"
instance_type          = "t2.micro"
subnet_id              = aws_subnet.private.id
vpc_security_group_ids = [aws_security_group.ec2_sg.id]

tags = {
Name = "Private-EC2"
}
}

![image.png](attachment:9503c32a-0a59-4676-9ac6-9a036cc3b493:image.png)



4. -Create one aws_s3_bucket per environment using for_each
Naming: myapp-<env>-<bucket_suffix>
-Enable versioning using aws_s3_bucket_versioning
Only when versioning = true
-Create IAM users from all environments
- Combine user lists
- Remove duplicates
-Create IAM policies dynamically per environment
- Allow access only to that environment's bucket
- Use jsonencode()
-Attach policies to users
- Users should only access their environment bucket
- Add lifecycle rules using dynamic block
- Use remote backend (S3 + DynamoDB)

ans : IAM not allowed in learner lab 

after applying the config , two s3 buckets are created for dev and prod environments with unique names. Versioning is enabled conditionally, lifecycle rules are applied

![image.png](attachment:53a095ee-1d9e-49d9-8e91-17201951cb38:image.png)

![image.png](attachment:1319285d-1608-4f60-b380-81ab0a9f6c6f:image.png)

lifecycle rule applied for both the buckets :

![image.png](attachment:c7a5d92f-e202-4721-b8f4-9a980eb03c2c:image.png)
