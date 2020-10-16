# Learning objective
Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service from AWS. In this lab, you will work with the AWS command line interface and console, using command line utilities like eksctl and kubectl to launch an EKS cluster, provision a Kubernetes deployment and pod running instances of nginx, and create a LoadBalancer service to expose your application over the internet.

Create an IAM User with Admin Permissions
Launch an EC2 Instance and Configure the Command Line Tools
Provision an EKS Cluster
Create a Deployment on Your EKS Cluster
Test the High Availability Features of Your EKS Cluster

# Create an IAM User with Admin Permissions
Create an IAM user with programmatic access and administrator-level privileges.
Take note of the access key and secret access key of your user because we will use them in the next step.

# Launch an EC2 Instance and Configure the Command Line Tools
Create an EC2 instance in us-east-1 region.

# If necessary, upgrade the AWS CLI on your EC2 instance to CLI v.2x or later.
Launch an EC2 (eks-admin-workstation) Instance and Configure the Command Line Tools Refer to upgrade aws cli use above created security key and password for AWS cli 
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html#cliv2-linux-upgrade

# Configure the AWS CLI using the credentials of the user you just created.
> aws configure

# Install eksctl on your EC2 instance.
https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

# Install kubectl on your EC2 instance.
https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

# Provision an EKS Cluster
Use eksctl to provision an EKS cluster with three worker nodes in us-east-1.
Use Kubernetes version 1.16 or later.
> eksctl create cluster --name dev-cluster --version 1.16 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1c,us-east-1d --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed

## To get cluster run eks-admin-workstation
>  eksctl get cluster

# Command which will enable us to connect with cluster, this will update configuration for kubectl
> aws eks update-kubeconfig --name dev-cluster --region us-east-1


# Create a Deployment on Your EKS Cluster
Course files can be found here: https://github.com/shijujohn1093/eksbasics
Use kubectl to create a LoadBalancer service.
Check the status of your LoadBalancer service using kubectl.
Use kubectl to create a Deployment on your EKS cluster, using the standard nginx image EKS has available in the default Docker Hub registry.
Check the status of your cluster, deployment, and pods using kubectl.
When the Deployment is up and running, check that you can access your application using the DNS name of the LoadBalancer.

## clone 
> git clone https://github.com/shijujohn1093/eksbasics
> cd eksbasics

## Use kubectl to create a LoadBalancer service
> kubectl apply -f ./nginx-svc.yaml

## Check the status of your LoadBalancer service using kubectl : This command will return reference of load balancer an dns address
> kubectl get service

## Use kubectl to create a Deployment on your EKS cluster, using the standard nginx image EKS has available in the default Docker Hub registry
> kubectl apply -f ./nginx-deployment.yaml

## Check the status of your cluster, deployment, and pods using kubectl.
### Command to get deployments
> kubectl get deployment

### Command to get pods, it will return 3 pods
> kubectl get pod

### Command to get replcia set, 3 out 3 should be running
> kubectl get rs

### Command to get nodes
> kubectl get node

## Now again run following commans and get dns address and check if its woking, you check same url on browser
> kubectl get service
> curl "<dns reurn by loadbalancer service>"

## Test node management by stopping ec2 instances from AWs console


# Deleting clusters
## Run following command to delete cluster
> eksctl delete cluster dev-cluster
## Go to AWS console delete all EC2 instances
## if you not longer need admin user, delete user from IAM



