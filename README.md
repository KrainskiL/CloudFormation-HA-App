# Udacity Cloud DevOps Engineer Project 2 - Udagram

Repository contains CloudFormation template and scripts for deployment of high availability web app Udagram.

Template `udagram.yml` creates both network and server infrastructure.

**Network infrastructure**
* VPC with two public and private subnet (one per Availability Zone)
* Internet Gateway with VPC attachment
* NAT Gateways with Elastic IP (one per public subnet)
* Public and private routing tables

**Servers infrastructure**
* Instance profile and role for EC2 instances allowing read access to S3 buckets
* Security group for App Load Balancer (allowed ingress and egress on port 80)
* Security group for webservers (allowed ingress on port 80 and 22, fully allowed egress)
* LaunchConfiguration creating `t3.medium` (2vCPU, 4GB RAM) instances with 10 GB storage and Ubuntu 18.04 LTS AMI
* Autoscaling group with minimum 4 webservers instances 
* Load Balancer with Listener, ListenerRule and TargetGroup 

**Usage**

1. Install [AWS CLI](https://aws.amazon.com/cli/)
2. Use the CloudFormation script:
   ```bash
   ./scripts/create.sh udagram-stack ./udagram.yml udagram-param.json
   ```
3. Check `Outputs` section of created stack in AWS Console. Public LoadBalancer URL should be displayed there.

![LoadBalancer Outputs](https://github.com/KrainskiL/CloudFormation-HA-App/blob/master/img/cloudformation_stack_output.PNG?raw=true)

4. Enjoy your high availability app!

![Udagram_app](https://github.com/KrainskiL/CloudFormation-HA-App/blob/master/img/udagram_mainpage.PNG?raw=true)

5. To delete stack use 
   ```bash
   ./scripts/delete.sh udagram-stack
   ```
