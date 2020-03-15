# AWSVPCSetup

<b>Project Requirements</b>: <p> Create an account with multiple VPC's. Write an IaaS template (AWS Cloudformation chosen here). Create Private and Public Subnets and demonstrate VPC Peering by querying an apache webserver across VPC's. Suggested time for completion 4 hours</p>

<b>Approach</b>:
  1. AWS Cloudformation was used, a new account was setup using Organization Units.
  2. Admin and Auditor roles were created. Auditor roles
  3. 2 VPC's (VPC1 and VPC2) were created.
  4. Subnet's were created. A privete Subnet in VPC1.
  5. For public subnet the default AWS VPC was used to save time. The default VPC already has route tables and internet gateway setup.
  6. VPC peering was performed by creating a VPC peering resource and editing the route tables.
  7. Two ec2 instances were created, one performing the function of a webserver displaying a simple  "Hello World" message ina  private subnet.
  8. The second EC2 instance (referred as  Ping or Healthcheck EC2) executes a simple curl command as part cron job and write the result to cloudwatch logs.
  9. EC2 instances were created as part of the the cloudformation template. A Userdata script bootstraps the application.
  10. The webserver EC2 has no IAM role while the HealthCheck EC2 ahs permissions to read and write to S3 and Cloudwatch logs.
  11. An IAM role was created for the HealthCheck EC2.
  12. IP address or private DNS address of the webserver can be obtained from coudformation using !GetAtt ApacheInstance.PrivateDnsName feature in cloudformation.

<b>Deviations from Suggested Plan</b>
  1. The default VPC was used as Private/Public VPC to save time.
  2. Logs were written to cloudwatch instead of S3. This was done as S3 is an object store and unable to edits to a file, which is what log files do. Cloudwatch logs can be transferred to S3 later. S3 access was however retained by the EC2 instance.
  3. Additional NAT Gatewaysa dn Public Subnets were needed to access yum repositories. There are several pother alternatives. Some of these operations were performed via console.

