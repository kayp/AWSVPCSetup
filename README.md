# AWSVPCSetup

<b>Project Outline</b>: <p> Create an account with multiple VPC's. Write an IaaS template (AWS Cloudformation chosen here). Create Private and Public Subnets and demonstrate VPC Peering by querying an apache webserver across VPC's.</p>

<b>Deliverable</b>: 
  1. [Cloudformation Template creating resources](https://github.com/kayp/AWSVPCSetup/blob/master/cftemplates/VPCResources.yml)
  2. AWS Read Only Console access for reviewer.
  
<b>Approach</b>:
  1. AWS Cloudformation was used, a new account was setup using Organization Units.
  2. Admin and Auditor roles were created. Auditor roles are READ only.
  3. 2 VPC's (VPC1 and VPC2) were created.
  4. 2 Subnet's were created in VPC1. A privete Subnet  and a Public Subnet in VPC1.
  5. A Public Subnet was created in VPC2.
  6. VPC peering was performed by creating a VPC peering resource and editing the route tables.
  7. Two ec2 instances were created, one performing the function of a webserver displaying a simple  "Hello World" message in a  private subnet.
  8. The second EC2 instance (referred as  Ping or Healthcheck EC2) executes a simple curl command as part cron job and write the result to cloudwatch logs.
  9. EC2 instances were created as part of the the cloudformation template. A Userdata script bootstraps the application.
  10. The webserver EC2 has no IAM role while the HealthCheck EC2 has permissions to read and write to S3 and Cloudwatch logs.
  11. An IAM role was created for the HealthCheck EC2.
  12. IP address or private DNS address of the webserver can be obtained from cloudformation using !GetAtt ApacheInstance.PrivateDnsName feature in cloudformation. Harcoding IP address is not necessary.

