# eks-terraform-test-deployment
Test repository for creating and deploying EKS cluster using terraform

Remediation use case statement: AWS EKS security groups allow incoming traffic only on TCP port 443.

Files Created:

1. vars.tf for storing environment variables such as AWS access key and secret access key.
2. main.tf for performing the AWS Configuration and to declare the AWS provider and the availability zone present in the declared region.
3. vpc.tf to create the AWS VPC. We are using the AWS VPC module for VPC creation. The code will create the AWS VPC of 10.0.0.0/16 CIDR range in ap-south-1 region. The VPC will have 3 public and private subnets and NAT Gateway & DNS Hostname is enabled
4. security.tf for creating AWS Security Group. We are creating 2 security groups for 2 worker node groups. We are allowing only 443 port for incoming traffic. Additioanlly, we are restricting the SSH access for 10.0.0.0/8 CIDR Block
5. eks.tf for EKS Cluster creation using the terraform AWS EKS module. The code will create 2 worker groups with the desired capacity of instances of type t2.micro. We are attaching the earlier created security group to both the worker node groups.
6. kubernetes.tf for declaring the terraform Kubernetes provider.
7. output.tf which will output the name of our cluster and expose the endpoint of our cluster.

Steps to run:

1. Update the vars.tf file with the AWS access key and the AWS Secret Key.
2. Run the terrform init command to initialize and download the provider plugins
3. Run terraform plan and apply conseqyesntly.

 Further improvements can be done to this project by writing ansible playbooks to create and run deploy kubernetes pods and services.

For Example: 
```
- name: Deploy to Kubernetes Cluster 
  hosts: all
  become: true
tasks:
  - name: Deploy Pod
    shell: |
      kubectl apply -f pod.yml
 
