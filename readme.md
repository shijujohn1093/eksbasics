# Learning objective
Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service from AWS. In this lab, you will work with the AWS command line interface and console, using command line utilities like eksctl and kubectl to launch an EKS cluster, provision a Kubernetes deployment and pod running instances of nginx, and create a LoadBalancer service to expose your application over the internet.

Create an IAM User with Admin Permissions
Launch an EC2 Instance and Configure the Command Line Tools
Provision an EKS Cluster
Create a Deployment on Your EKS Cluster
Test the High Availability Features of Your EKS Cluster

# Create I with admin rights

# Launch an EC2 (eks-admin-workstation) Instance and Configure the Command Line Tools Refer to upgrade aws cli use above created security key and password for AWS cli 
https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html#cliv2-linux-upgrade

# Install kubectl
https://docs.aws.amazon.com/eks/latest/userguide/install-kubectl.html

# install ekdctl
https://docs.aws.amazon.com/eks/latest/userguide/eksctl.html

# Create cluster using following command
> eksctl create cluster --name dev-cluster --version 1.16 --region us-east-1 --zones=us-east-1a,us-east-1b,us-east-1c,us-east-1d --nodegroup-name standard-workers --node-type t3.micro --nodes 3 --nodes-min 1 --nodes-max 4 --managed

# To get cluster run eks-admin-workstation
>  eksctl get cluster

# Command which will enable us to connect with cluster, this will update configuration for kubectl
> aws eks update-kubeconfig --name dev-cluster --region us-east-1

# clone 
> git clone https://github.com/shijujohn1093/eksbasics
> cd eksbasics

# create aws load balancer service
kubectl apply -f ./nginx-svc.yaml

# kubectl get service : This command will return reference of load balancer an dns address
> kubectl get service

# Deploy container and pod
kubectl apply -f ./nginx-deployment.yaml

# Command to get deployments
> kubectl get deployment

# Command to get pods, it will return 3 pods
> kubectl get pod

# Command to get replcia set, 3 out 3 should be running
> kubectl get rs

# Command to get nodes
> kubectl get node



