# aws-codepipeline-bluegreen-swiggy
Deployment strategy (Blue-Green) implemented using AWS CodePipeline for the Swiggy website.

## Introduction

In the realm of modern software development, DevSecOps practices are gaining prominence for their emphasis on integrating security seamlessly into the software development lifecycle. One critical aspect of this approach is implementing efficient deployment strategies that not only ensure reliability but also maintain security standards. In this blog post, we will delve into the concept of Blue-Green deployment and demonstrate how to apply it to a Swiggy-clone application hosted on AWS ECS (Elastic Container Service) using AWS CodePipeline.

## What is Blue-Green Deployment?

Blue-Green deployment is a technique used to minimize downtime and risk during the release of new versions of an application. In this approach, two identical production environments, termed ‘Blue’ and ‘Green’, are maintained. At any given time, only one environment (e.g., Blue) serves live traffic while the other (e.g., Green) remains idle. When a new version is to be deployed, the new version is deployed to the idle environment (Green). Once the deployment is validated, traffic is seamlessly switched to the updated environment (Green), allowing for quick rollback to the previous version if issues arise.

## Setting up AWS ECS for Swiggy-Clone

To demonstrate Blue-Green deployment, we’ll use AWS ECS to host our Swiggy-clone application. ECS is a highly scalable container orchestration service provided by AWS.

## Implementing Blue-Green Deployment with AWS CodePipeline

AWS CodePipeline is a fully managed continuous integration and continuous delivery (CI/CD) service that automates the build, test, and deployment phases of your release process. Let’s see how to set up a Blue-Green deployment pipeline using AWS CodePipeline:

1. **Source Stage**: Connect your CodePipeline to your source code repository (e.g., GitHub). Trigger the pipeline when changes are detected in the repository.

2. **Build Stage**: Use AWS CodeBuild to build your Swiggy-clone Docker image from the source code. Run any necessary tests during this stage.

3. **Deploy Stage**: Configure AWS CodeDeploy for ECS to manage the deployment of your application to ECS clusters. Here’s where Blue-Green deployment strategy comes into play:
   - Define two ECS services: Blue and Green.
   - Use CodeDeploy to deploy the new version of your Swiggy-clone application to the Green service.
   - After deployment, automate the ALB routing to gradually shift traffic from the Blue service to the Green service based on predefined health checks.
   - Monitor the deployment process and rollback automatically if issues occur during the transition.

## GitHub Repository

Find the GitHub repository for this project at: [Swiggy_clone GitHub Repo](https://github.com/Abrar-Akbar/aws-codepipeline-bluegreen-swiggy.git)

## Step-by-Step Setup Guide

Follow these steps to set up your environment for Blue-Green deployment:

1. **Create a Sonar Server**: Detailed instructions provided in the setup guide.
 ```bash
  sh install_docker.sh
   ```
 ```bash
 sh install_trivy.sh
   ```
 ```bash
 sh run_sonarqube.sh
   ```
## Aditional If setup Proxy Manager
 ```bash
  docker-compose up -d 
  ```
2. **SonarQube Set-Up**: Customizing SonarQube for your project.
3. **Create AWS Code Build Project**: Setting up the AWS CodeBuild project.
4. **ECS Cluster Creation**: Creating the ECS cluster.
5. **ECS Task Definition Creation**: Defining tasks for ECS.
6. **Load Balancer Creation**: Setting up the load balancer.
7. **ECS Service Creation**: Creating the ECS service.
8. **AWS Code Pipeline Creation**: Setting up the continuous deployment pipeline.
9. **ECS Deployment**: Deploying the application to ECS.
10. **Clean Up**: Properly cleaning up resources after completion.

Refer to the detailed instructions in the setup guide for each step.

## Conclusion

By following the steps outlined in this guide, you can implement Blue-Green deployment for your Swiggy-clone application hosted on AWS ECS using AWS CodePipeline. This approach enhances reliability, minimizes downtime, and maintains security standards throughout the deployment process. For further details and assistance, refer to the setup guide provided in the repository.

**Note**: Please ensure to follow the cleanup steps to avoid any unnecessary charges and resource usage.
