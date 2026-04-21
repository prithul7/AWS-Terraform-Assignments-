1. Configure S3 Static Website:
- Create an S3 bucket
- Enable static website hosting
- Upload an HTML page
- Configure bucket policy for public read access
- Enable versioning

![image.png](attachment:861d0cfc-25c5-4b86-b920-e8d951aa3a0e:image.png)

2. Implement IAM Best Practices
- Create IAM groups: Admin, Dev, ReadOnly
- Apply least privilege policies
- Enable MFA for root
- Create custom policy for S3 restricted folder access

created 3 IAM users and attached 3 groups with different permissions

![image.png](attachment:e70f7016-31e2-479e-8609-2469e511da87:image.png)

created 3 groups with different permissions 

![image.png](attachment:71703975-c99f-4369-8799-226361aa3a7b:image.png)

IAm user prithul-admin given prithul-admin-group permissions :-

![image.png](attachment:cb069e7b-787d-464d-8ede-da0a1456e4ed:image.png)

3. Enable CloudWatch Monitoring
- Create CPU utilization alarm
- Trigger SNS notification
- Monitor ALB metrics
- Enable detailed monitoring for EC2

CPU utilization reaching threshold 70%

![image.png](attachment:07c4025a-866f-4bf0-9e18-fa1089001f6e:image.png)

got an email on CPU hike 

![image.png](attachment:f1d53a4b-b32a-46ec-8c31-066be20067ea:image.png)

4. RDS Deployment:
- Launch RDS MySQL in private subnet
- Configure DB Subnet Group
- Enable Multi-AZ
- Enable automated backups
- Connect from EC2 App server

created db subnet group :

![image.png](attachment:41e2db35-8b6c-403c-91bf-2d3a2d042943:image.png)

connected successfullly:

![image.png](attachment:d5d4c289-2721-40b9-9a6d-1c0715285099:image.png)

5. Disaster Recovery Setup Enable:
- S3 Cross-Region Replication
- RDS Read Replica
- AMI backup
- Simulate region failure

![image.png](attachment:6a1f92c0-10ae-42cb-ac21-a64f8af2a1d4:image.png)

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

![image.png](attachment:144b6615-5de8-44af-beae-fe540b6a3009:image.png)

2 subnets created 

![image.png](attachment:b985f9ab-41fe-4329-90d5-b378962075b5:image.png)

hub-Spoke1 peering connection

![image.png](attachment:4bb25a25-958a-4bec-8e60-c4a9de1a1392:image.png)

hub-Spoke2 peering connection

![image.png](attachment:283b7eef-597f-46ed-991a-ae033e981187:image.png)

3 rts for control traffic 

![image.png](attachment:8a7717b3-88ab-4060-9dd3-86a35bc75e23:image.png)
