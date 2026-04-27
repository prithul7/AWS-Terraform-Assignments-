1. Configure S3 Static Website:
- Create an S3 bucket
- Enable static website hosting
- Upload an HTML page
- Configure bucket policy for public read access
- Enable versioning

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/8c90901fe611f9aa17e4044a587e3fdfa2bc8fc1/image.png)

2. Implement IAM Best Practices
- Create IAM groups: Admin, Dev, ReadOnly
- Apply least privilege policies
- Enable MFA for root
- Create custom policy for S3 restricted folder access

created 3 IAM users and attached 3 groups with different permissions

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image2.png)

created 3 groups with different permissions 

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image3.png)

IAm user prithul-admin given prithul-admin-group permissions :-

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image4.png)

3. Enable CloudWatch Monitoring
- Create CPU utilization alarm
- Trigger SNS notification
- Monitor ALB metrics
- Enable detailed monitoring for EC2

CPU utilization reaching threshold 70%

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image5.png)

got an email on CPU hike 

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image6.png)

4. RDS Deployment:
- Launch RDS MySQL in private subnet
- Configure DB Subnet Group
- Enable Multi-AZ
- Enable automated backups
- Connect from EC2 App server

created db subnet group :

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image7.png)

connected successfullly:

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image8.png)

5. Disaster Recovery Setup Enable:
- S3 Cross-Region Replication
- RDS Read Replica
- AMI backup
- Simulate region failure

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image9.png)

6. Build a Hub-and-Spoke VPC Architecture

Create:

- 1 Hub VPC
- 2 Spoke VPCs
- Connect them using VPC Peering

Ensure:

- Spoke1 can talk to Hub
- Spoke2 can talk to Hub
- Spoke1 CANNOT talk to Spoke2
- Use route tables to control traffic

3 vpc created 

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image10.png)

2 subnets created 

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/imag11.png)

hub-Spoke1 peering connection

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image12.png)

hub-Spoke2 peering connection

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image13.png)

3 rts for control traffic 

![image.png](https://github.com/prithul7/AWS-Terraform-Assignments-/blob/2de8770c250f30c9f3d654e4bf175d3e0ae16cda/image14.png)
