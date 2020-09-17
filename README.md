
Azure using ARM

[WordPress with SQL Replication]

(https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fwordpress-mysql-replication%2Fazuredeploy.json)


[AKS]
(https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-aks-advanced-networking%2fazuredeploy.json)


AWS using CloudFormation

WordPress Multi-AZ

Filename - WP Multi-AZ VMs.yaml

Download WP Multi-AZ VMs.yaml to local computer
Log in to AWS

Using Default VPC with subnets, IGW already set up
Create SSH EC2 key pair

Select:
 CloudFormation
   Create Stack
    Template is ready
	Upload a template file
	Choose WP Multi-AZ VMs.yaml
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


NOTE:

PHP version in CloudFormation template is too old for version of WordPress so needs updating. Wordpress webpage does not show up but is reachable



EKS
