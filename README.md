# EFK-on-kubernetes

Pre-requisites: Install EKS ctl:
-------------------------------
$ cat script.sh 

ARCH=amd64

PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin

---------------------
# Install CSI DRIVER to create EBS volumes (pv) automatically - 

$eksctl create addon --name aws-ebs-csi-driver --cluster main-eks --region us-west-1

$kubectl get csidrivers

---------------------

first create namespaces using ns.yml, then deploy the remain code

steps to deploy:

Introduction: 
In the world of modern application development, efficient log management and analysis are crucial for ensuring the health and stability of your Kubernetes infrastructure. Elastic Stack, often referred to as EFK (Elasticsearch, Fluentd, and Kibana), is a powerful open-source solution that provides a robust logging and monitoring platform. In this blog post, we will walk you through the process of deploying EFK on Kubernetes, enabling you to centralize logs, gain valuable insights, and troubleshoot issues effectively.

Table of Contents:

1.Preparing Your Kubernetes Cluster for EFK Deployment

2.1. Installing Elasticsearch
2.2. Setting up Fluentd
2.3. Configuring Kibana

3.Deploying EFK Components on Kubernetes
   
3.1. Creating a Namespace
3.2. Deploying Elasticsearch
3.3. Setting up Fluentd
3.4. Deploying Kibana

4.Configuring Fluentd to Collect and Forward Logs

4.1. Fluentd ConfigMap
4.2. Fluentd DaemonSet
4.3. Verifying Fluentd Configuration

Visualizing and Analyzing Logs with Kibana

5.1. Accessing the Kibana Dashboard
5.2. Index Patterns and Data Visualization
5.3. Building Dashboards and Visualizations
