# CI/CD Pipeline for User Registration App with Jenkins

This approach is to set up an end-to-end CI/CD pipeline for a User Registration App using **Jenkins**, **Maven**, and **Tomcat Server**.

---

## Prerequisites

- **Infrastructure**:
  - Jenkins installed and running on a server (local or cloud).
  - Tomcat server installed and configured (local or remote).
- **Code repository**: Application source code hosted on GitHub.
- **Maven**: Installed on the Jenkins server.
- **Jenkins Plugins**:
  - Git Plugin
  - Maven Integration Plugin
  - Deploy to Container Plugin

---

## Step 1: Configure the Tomcat Server

1. **Enable Tomcat Manager**:
   - Open the `tomcat-users.xml` file in the `conf` directory of your Tomcat installation.
   - Add the following lines to create a manager role and user:
     ```xml
     <role rolename="manager-gui"/>
     <role rolename="manager-script"/>
     <user username="admin" password="admin" roles="manager-gui,manager-script"/>
     ```
   - Restart the Tomcat server.
   
     ![apache setup](https://github.com/user-attachments/assets/6fb0af0c-7ad2-483f-a096-4433cc89ee3a)


2. **Verify Manager Access**:
   - Open `http://<yours_tomcat_server>:8080/manager` in your browser and log in with the credentials.

---

## Step 2: Set Up Jenkins

1. **Install Required Plugins**:
   - Go to `Manage Jenkins > Plugins > Available Plugins` and install:
     - Git Plugin
     - Maven Integration Plugin
     - Deploy to Container Plugin

2. **Configure Global Tools**:
   - Navigate to `Manage Jenkins > Global Tool Configuration`:
     - Add Maven and provide the Maven home path.
     - Configure JDK if not already set up.

---

## Step 3: Create a Jenkins Pipeline Job

1. **Create a New Pipeline**:
   - In Jenkins, click `New Item` and select `Pipeline`.
   - Provide a name, e.g., `User Registration App CI/CD`.

2. **Configure the Pipeline**:
   - Define the pipeline script (details below).
   - Install Required Jenkins Plugins
     
**To set up the necessary plugins, go to Manage Jenkins > Manage Plugins and install:**
   - Maven Integration Plugin
   - Docker Pipeline Plugin
   - Kubernetes CLI Plugin
   - GitHub Plugin (if using GitHub)
   - Configure Jenkins
   - Go to Manage Jenkins > Configure System.
   -  Add your Maven and Docker configurations:
   - Specify Maven installation.
Set up the Docker daemon connection.

![maven build](https://github.com/user-attachments/assets/e6f22e1d-3b53-4e36-affc-a4233347cae1)

## Step 4: Git Repository Structure
   - Create your Git repository with the following components:

    **pom.xml:** Maven configuration for building the project.
    **Dockerfile:** Instructions for building the Docker image with Tomcat.
    **Jenkinsfile:** Jenkins pipeline configuration.
    **kubernetes/deployment.yaml:** Kubernetes configuration for deploying the application.
## Step 5: Create Dockerfile
   - Create a Dockerfile that will package your application into a Docker image:

     ![ec2](https://github.com/user-attachments/assets/0a91528d-a668-403e-bee7-5b758d08d4ac)

## Step 6: Kubernetes Deployment Configuration
   - In the kubernetes/deployment.yaml file, define the Kubernetes deployment and service:
## Step 7: Setting Up Docker and Kubernetes on Jenkins
**Docker Setup on Jenkins**
Install Docker on the Jenkins node:

```
sudo apt install docker.io
```
**Kubernetes CLI on Jenkins**
Install Kubernetes CLI on Jenkins:
```
sudo apt install kubectl

```
**Kubernetes Plugin Configuration in Jenkins**
Go to Manage Jenkins > Manage Plugins and install the Kubernetes CLI plugin.
Set up Kubernetes credentials in Jenkins to allow deployment.
## Step 8: Run the Pipeline
Once your Jenkinsfile, Dockerfile, and Kubernetes configurations are in place, you can trigger the pipeline manually or automatically using webhooks (e.g., from GitHub).

![jenkins build](https://github.com/user-attachments/assets/321b70ff-408b-4397-97b8-42599f2649ed)


**The Pipeline Will:**
Clone: Pull the source code from the Git repository.
Build: Use Maven to build the WAR file.
Docker Build: Build a Docker image and push it to Docker Hub.
Kubernetes Deployment: Deploy the application to the Kubernetes cluster.
## Access the Application

![register app deployment](https://github.com/user-attachments/assets/c7b60a28-43ac-4cc3-9685-d8940f29b553)



