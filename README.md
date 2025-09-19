# Radius Hub Application Deployment with Jenkins, Terraform, and AWS EC2

This project demonstrates the end-to-end deployment of a **Radius Hub Application** on **AWS EC2** instances using **Jenkins (CI/CD pipeline)** and **Terraform (Infrastructure as Code)**. The application Docker images are hosted on **GitHub Container Registry (ghcr.io)**, and the deployment pipeline is fully automated through Jenkins.

***

## Prerequisites

- AWS Account with IAM access for EC2 and related resources
- EC2 or Docker environment to run Jenkins
- Terraform installed (can be handled by Jenkins pipeline)
- GitHub repository containing:
    - Terraform configuration files
    - Application deployment code (Docker setup, provisioning scripts, etc.)

***

## Jenkins Setup

Jenkins can be run either:

- Inside **Docker** container, or
- Directly installed on a machine.

After installation, install the following **suggested plugins**:

- Git Plugin
- Credentials Binding Plugin
- AWS Credentials Plugin
- GitHub Branch Source Plugin
- Pipeline Plugin

***

## Jenkins Credentials

Create the following credentials in Jenkins:

- **github-creds** (optional) → GitHub username/password or token
- **env_file** → Secret file containing environment variables (.env file)
- **my-aws-creds** → AWS access key ID and secret access key
- **ghcr-creds** → GitHub Container Registry credentials (username and PAT)

***

## Pipeline Flow

The Jenkins pipeline automates both **infrastructure provisioning** and **application deployment**.

### Pipeline Stages

- **StageCheckout SCM**
- **StageCheckout Code**
- **StagePrepare .env from Secret File**
- **StagePrepare Terraform Files**
- **StageTerraform Init**
- **StageTerraform Plan**
- **StageTerraform Apply**
- **StageGet Terraform Outputs**
- **StageDeploy App on EC2**
- **StagePost Actions**

Once completed, the application will be **accessible on AWS EC2**.



## Destroy Pipeline

To clean up and destroy all AWS infrastructure created by Terraform, a separate **destroy pipeline** is created using a `Jenkins-destroy` file.

***

## Conclusion

- Jenkins pipelines automate the **infrastructure provisioning** and **deployment** of the Radius Hub Application.
- Application images are securely pulled from **ghcr.io** and deployed on **AWS EC2**.
- A dedicated destroy pipeline ensures that AWS resources are properly cleaned up when no longer needed.

***


