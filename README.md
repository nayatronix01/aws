## CloudFormation templates for HA with VMs and HA with Containers. 
All templates were downloaded from the internet  

## WordPress HA  

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


## EKS WordPress HA  


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



## Deploy WordPress Helm Chart with  HA RDS(MariaDB)  

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


## NOTES  
Issue with EKS CF helm chart deployment. KubeGetLambdaArn does not appear in stack output or in CF template This will require further investigation.  WP Helm install can be done manually by SSH to bastion host and installing helm, then running chart or by importing cluster in Rancher and using WP Helm chart in apps.  
A pipeline can be configured to automate CF deployment.  
I have used Azure once before and the timeframe for this requirement and getting up to speed with Azure is too short. I investigated and found that Azure Resource manager is used to deploy templates in Azure. The templates below can be used to deploy the services in Azure:  


[WordPress with SQL Replication]

(https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fwordpress-mysql-replication%2Fazuredeploy.json)

[AKS] 
(https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-aks-advanced-networking%2fazuredeploy.json)

