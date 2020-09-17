Used CloudFormation templates from the internet

WordPress HA

Filename - wp-multi-az-vms.yaml

Download wp-multi-az-vms.yaml to local computer
Log in to AWS

Create SSH EC2 key pair

Select:
 CloudFormation
   Create Stack
    Template is ready
	Upload a template file
	Choose wp-multi-az-vms.yaml
Click on Next

Enter Stack name
Edit parameters as required.
Parameters to note:

Select EC2 Key pair
MultiAZDB should be set to true
WebServerCapacity should be set to 2
SSH location 0.0.0.0/0 
Select Subnets - at least 2 for Multi-AZ
Select VPC id that hosts above subnets

Click Next
Click Next
Create Stack

Once stack create is complete
Select stack name
Select Outputs Tab
Copy URL into web browser


EKS WordPress HA

Filename - amazon-eks-master.template.yaml (if not using Quick Launch links)

[EKS Quick Launch New VPC](https://fwd.aws/6dEQ7)
[EKS Quick Launch Existing VPC](https://fwd.aws/e37MA)

Click on one of links above
Log in to AWS


Click on Next

Enter Stack name if not entered already
Edit parameters as required.
Parameters to note:

Provision bastion host
SSH key name
EKS public access endpoint - enabled
ALB ingress controller - enabled
Cluster autoscaler - enabled

Click Next
Click Next
Create Stack

Once stack create is complete
Select stack name
Select Outputs Tab

Make note of the following:
KubeClusterName
KubeGetLambdaArn
NodeGroupSecurityGroupId
BastionSecurityGroupId



DEPLOY WORDPRESS HELM CHART WITH EXTERNAL DB

Download eks-helm3-wordpress-deploy-RDS.yaml

Log into AWS

Select:
 CloudFormation
   Create Stack
    Template is ready
	Upload a template file
	Choose eks-helm3-wordpress-deploy-RDS.yaml
	
Click on Next

Fill in Parameters:

KubeClusterName
KubeGetLambdaArn
Namespace
Name
wordpressPassword
DBMasterUserPassword
NodeGroupSecurityGroupId
BastionSecurityGroupId
Subnet1ID - (Select a private subnet from the main EKS stack.)
Subnet2ID - (Select a different private subnet from the main EKS stack.)
VPCID - (Select the EKSStack VPC)

Click Next
Click Next
Create Stack

Once stack create is complete
Select stack name
Select Outputs Tab
Get the value of WPElbHostName
In your preferred browser, enter the value of WPElbHostName
Under the Meta section of the page, choose Log in
Enter the WordPress Username and Password you created in the stack creation



