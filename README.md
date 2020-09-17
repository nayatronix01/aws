
Azure using ARM

[WordPress with SQL Replication]

(https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fwordpress-mysql-replication%2Fazuredeploy.json)


[AKS]
(https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-aks-advanced-networking%2fazuredeploy.json)


AWS using CloudFormation

WordPress Multi-AZ

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


EKS


[EKS Quick Launch New VPC](https://fwd.aws/6dEQ7)

Download amazon-eks-master.template.yaml to local computer

Click on link above
Log in to AWS


Create SSH EC2 key pair

Select:
 CloudFormation
   Create Stack
    Template is ready
	Upload a template file
	Choose amazon-eks-master.template.yaml
Click on Next

Enter Stack name
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

Select:
 CloudFormation
   Create Stack
    Template is ready
	Upload a template file
	Choose amazon-eks-master.template.yaml
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



