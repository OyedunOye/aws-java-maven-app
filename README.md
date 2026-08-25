
# Deployment to EC2 Server from Jenkins Pipeline (CI/CD)

This project focuses on the use of AWS services as deployment host for applications.


## Get Repo Locally

Clone the project

```bash
  git clone https://github.com/OyedunOye/aws-java-maven-app.git
```

Go to the project directory

```bash
  cd aws-java-maven-app
```

## Tech Stack

**Cloud Services:** AWS EC2, IAM, VPC, Subnet, Public IPv4, Security Group

**Tools:** Jenkins, Docker, Git, GitHub, DockerHub


## Documentation

### Project Overview

The aim is to include the CD part of CI/CD pipeline in this project. AWS EC2 is the host server for the deployment of applications in this project. The server instance was provisioned via AWS console in N. Virginia region VPC and us-east-1d AZ. SSH key was set up for accessing the server and firewall rules configured in security group to open needed ports for connection traffic. Docker was installed on the server and server access credentials was configured for this server in Jenkins.

#### Plugins Installed and Configured for This project

In addition to the previously configured plugins in the CI part of Jenkins pipeline, the following plugin was installed for this CD continuation:

- SSH agent

#### Credentials Configured within Jenkins Pipeline for This Project

- ec2-server-key (SSH username with private key)


### Features explored and Jenkinsfile for each

The project has 5 branches asides the master branch. Each branch showcases different Jenkins job documented below:
- starting-code: This branch has a simple Jenkinsfile configured to create a multi-branch pipeline. No further implementation happened here.
- jenkins-connect-ec2: This branch focused on the deploy stage where connection to the created EC2 instance is configured. The Jenkinsfile was configured to pull and run a manually built image of a React-app from private DockerHub repo into EC2 instance. This seamlessly run in the server and container port opened for browser access to this deployed app.
- jenkins-complete-pipeline: configures Jenkinsfile with the complete build steps, including reusing some functions from a [shared jenkins library](https://github.com/OyedunOye/jenkins-shared-library.git). This branch's Jenkinsfile combine the whole CI/CD stages in a pipeline and successfully automate CI/CD by Jenkins.
- jenkins-deploy-with-docker-compose: the Jenkinsfile executes docker-compose up command to start more than a single container at once. This showcases real life app deployment reality. This required the installation of docker-compose on EC2 instance and copy of docker-compose.yaml file into the EC2 instance. For better code organization, the docker-compose command and other shell commands to be run in EC2 bash shell were extracted into a shell script and this script was run in bash once while jenkins ssh into the EC2 instance.
- jenkins-complete-pipeline-with-dynamic-inc-docker-image-version: 2 more stages were added here. A stage to dynamically increase the version of app in pom.xml. This is placed before all stages needing image_name to ensure that newly generated docker image is ultimately deployed for each build. The second is a last commit version bump stage which updates pom.xml file in git repo so that the next build could have access to the previous version number and correctly calculate the next version number.

## Screenshots

![Jenkins Job List](https://res.cloudinary.com/dpav6x91z/image/upload/v1787622423/Screenshot_2026-08-25_034051_qkb1ga.png)
![AWS CD Multibranch Pipeline](https://res.cloudinary.com/dpav6x91z/image/upload/v1787661647/aws-ci-cd-multibranch-pipeline_sguwqm.png)
![React App Deployed by Jenkins Pipeline](https://res.cloudinary.com/dpav6x91z/image/upload/v1787622557/Screenshot_2026-08-24_234702_sc3f8x.png)
![Java Maven App Deployed by Jenkins Pipeline](https://res.cloudinary.com/dpav6x91z/image/upload/v1787622639/Screenshot_2026-08-25_035005_nakezd.png)
