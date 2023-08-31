### CircleCI Status
[![CircleCI](https://dl.circleci.com/status-badge/img/gh/phan-van-thuy/udacity_final/tree/master.svg?style=svg)](https://dl.circleci.com/status-badge/redirect/gh/phan-van-thuy/udacity_final/tree/master)

## Load Balancer Endpoint
http://a0c3225907c1c425a94cd4e4eb161ec8-1385643172.us-east-1.elb.amazonaws.com/

## github link

- https://github.com/phan-van-thuy/udacity_final/tree/master

## dockerhub link
- https://hub.docker.com/repository/docker/thuydocker/final/general
# Udacity Capstone Project

In this project you will apply the skills and knowledge which were developed throughout the Cloud DevOps Nanodegree program. These include:

* Working in AWS
* Using Circle CI to implement Continuous Integration and Continuous Deployment
* Building pipelines
* Working with CloudFormation to deploy clusters/infrastructure
* Building Docker containers in pipelines
* Building Kubernetes clusters

## Project Scope

## Environment Variables

To run this project, you will need to add the following environment variables to your CircleCI environment variables

* `AWS_DEFAULT_REGION`
* `AWS_ACCESS_KEY_ID`
* `AWS_SECRET_ACCESS_KEY`
* `DOCKER_PASSWORD`
* `DOCKER_USERNAME`

## Folder structure

| File | Description |
| ---- | ----------- |
| `.circleci/config.yml` | CircleCI configuration |
| `cloudformation` | CloudFormation yaml templates for creating infrastructure |
| `cloudformation/deployt-eks.yaml` | Create EKS cluster |
| `cloudformation/server-parameters.json` | Create EKS cluster params |
| `k8s` | Kubernetes resource files |
| `k8s/deployment.yml` | Kubernetes deployment declaration |
| `k8s/aws-authen-cm.yml` | Kubernetes configmap declaration |
| `app.py` | main application to answer request |
| `Dockerfile` | Dockerfile to build image|
| `Makefile` | Build file of the project |
| `requirements.txt` | Python required libraries |


## Run Steps For Cloud Deployment
* Create a DockerHub public repository
* Run `aws cloudformation deploy --template-file deployt-eks.yml --stack-name Capstone-project  --tags project=udapeople --capabilities CAPABILITY_NAMED_IAM` to create EKS cluster
* Run `aws eks list-clusters` to see output like below
`{
    "clusters": [
        "Capstone-project-EKS"
    ]
}` 
to get cluster name
* Replace the line `- arn:aws:iam::522103081893:role/Capstone-project-EKS-WorkerNodesRole-197K0794U0W3K` in `aws-authen-cm.yml`
* Configure CircleCI project for the github repository
* Done!

* Some kubectl commands to check k8s resources
```bash
    # Fet k8s configs
    aws eks --region us-east-1 update-kubeconfig --name Capstone-project-EKS
    # check all 
    kubectl get all

Remember to replace names of DockerHub repository & cluster name to the script file before you run.
