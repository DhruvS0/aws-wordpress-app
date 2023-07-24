# aws-wordpress-app
Deploying a highly available Wordpress application in a single region using a Multi-AZ MySQL database and CPU-based auto-scaler.
![Slide1](https://github.com/DhruvS0/aws-wordpress-app/assets/113872537/1aa1f4b6-f0cd-433f-9fbc-9b9760217841)

The AWS Services that are used in this project are:

**AWS Identity and Access Management(AWS IAM) -** securely manage identities and access to AWS services and resources

**Amazon Virtual Private Cloud(Amazon VPC) -** define and launch AWS resources in a logically isolated virtual environment

**Amazon Elastic Compute Cloud(Amazon EC2) -** provides scalable computing capacity

**Amazon Relational Database Service(Amazon RDS) -** fully managed, open-source cloud database service that allows you to easily operate and scale your relational database

**Amazon Simple Storage Service(Amazon S3) -** object storage service offering industry-leading scalability, data availability, security, and performance

**Amazon Elastic File System (Amazon EFS) -** serverless, fully elastic file storage

**AWS Simple Systems Manager(SSM) -** operations hub for your AWS applications and resources and a secure end-to-end management solution

**AWS Secrets Manager -** manage, retrieve, and rotate database credentials, tokens, API keys, and other secrets

**AWS Certificate Manager(ACM) -** provision and manage SSL/TLS certificates with AWS services and connected resources

**Amazon CloudFront -** content delivery network (CDN) service built for high performance, security, and developer convenience

## Resources created in the project -
### Creating input variables, provider, local values and data sources
#### Input Variables
**az_num -** Set the number of availability zones to use

**namespace -** Set a prefix for the resource names

**vpc_cidr_block -** Set the IP address block for the virtual private cloud (VPC)
#### Provider
**aws -** Set the minimal provider version and default resource tags

**Local Values -** temporary localized variables of common configs
#### Data Sources
**aws_region -** Get the current region

**aws_availability_zones -** Get list of availability zones

**aws_ami -** Get a specific Linux Amazon machine image (AMI)

**aws_iam_policy -** Get a specific Identity and Access Management (IAM) policy

**aws_iam_policy_document -** Generate a IAM policy document to allow EC2 to assume a role

Create the necessary IAM resources, that will allow your EC2 instances to read from an S3 bucket, as well get full access permissions to the RDS resources.

#### Creating Resources for IAM
**aws_iam_role -** Create an IAM Role

**aws_iam_instance_profile -** Create an IAM EC2 Instance profile of a IAM role to attach to an EC2 instance

#### Creating Resources for Network

**aws_vpc -** Create a default VPC

**aws_subnet -** Create a subnet within a VPC

**aws_internet_gateway -** Allow communication between VPC and the internet

**aws_route_table -** Create a routing table to control where the network traffic is directed

**aws_main_route_table_association -** Set the default network routing table for the default VPC

**aws_route_table_association -** Associate the route table to a VPC subnet

**aws_nat_gateway -** Create a Network Address Translation (NAT) gateway to allow private subnet to access services

**aws_eip -** Create an Elastic IP (EIP) for the NAT Gateways

#### Creating Resources for Security
**aws_security_group -** Create a security group that controls the traffic that is allowed to reach and leave the resources

**aws_vpc_endpoint -** Create a VPC endpoint (VPCE) enables customers to privately connect to supported AWS services

#### Create Resources for Application
We will now be able to deploy the resources we need to host our application i.e., have created an RDS MySQL database, a load balancer, an autoscaling group, an EFS file system, an S3 bucket, and many more resources.

**aws_db_subnet_group -** Create a subnet group for database across availability zones

**random_password -** Create a random password

**aws_secretsmanager_secret -** Create a Secrets Manager entry

**aws_secretsmanager_secret_version -** Create a value for the Secrets Manager entry

**aws_db_instance -** Create a MySQL database

**aws_efs_file_system -** Create an EFS volume

**aws_efs_mount_target -** Create a configuration where the EFS volume to a set of instances

**aws_instance -** Create an EC2 that bootstrap the Wordpress application

**aws_ami_copy -** Create a copy of the Amazon Machine Image (AMI) being used

**aws_lb -** Create a application load balancer (ALB) for the Wordpress web application

**aws_launch_template -** Create a launch template that hosts the Wordpress web application

**aws_autoscaling_group -** Create a auto-scaler group that scale the Wordpress web application instances

**aws_autoscaling_policy -** Create a auto scaling policy

**aws_cloudwatch_metric_alarm -** Create a CloudWatch Metric Alarm

**aws_lb_target_group -** Create a target group to attach the load balancer for the Wordpress web application

**aws_lb_listener -** Create a load balancer listener for the ALB

**tls_private_key -** Create a TLS private key

**tls_self_signed_cert -** Create a public TLS certificate signed by the private key

**aws_acm_certificate -** Create an ACM certificate entry with the TLS public certificate and private key

**aws_s3_bucket -** Create a private S3 Bucket

**aws_s3_bucket_public_access_block -** Create a public access block which disable public access for the private S3 Bucket

**aws_s3_object -** An object of S3, typically represent data similar file

**aws_cloudfront_distribution -** Create a CloudFront distribution for the Wordpress web application

**aws_cloudfront_cache_policy -** Create a CloudFront cache policy for the Wordpress web application

#### Creating Outputs for Application
Output Variables make information about your infrastructure available on the command line, and can expose information for other Terraform configurations to use. Output Variables are similar to return values in most programming languages. In our use case, we want to expose the endpoints of our Load Balancer and our CloudFront distribution, so we can test if our application has been deployed correctly.

**alb_endpoint_uri -** Application Load Balancer Uniform Resource Identifier

**alb_endpoint_url -** Application Load Balancer Uniform Resource Locator

**cloudfront_endpoint_url -** CloudFront Uniform Resource Identifier

## Steps to be followed:
1. Before running all the commands, it is best to configure the aws credentials by passing it through **aws configure** command.
1. Run the command **terraform init** to fetch the provider to create resources
1. Run the command **terraform validate** to validate syntax
1. Run the command **terraform plan** to plan the deployment
1. Run the command **terraform apply** to apply the deployment
1. Run the command **terraform destroy** to delete the infrastructure deployed.
