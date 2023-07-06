# Multi Branch EndToEnd Pipeline
<!-- ABOUT THE PROJECT -->
## About The Project

This project focuses on automating the deployment process for a web application using a CloudOps pipeline. The pipeline is built with Jenkins and Docker, enabling efficient code delivery and deployment to a production server.<br />

* Code Submission: Developers push their code to the central repository.
* Jenkins Slave Node: The code is cloned into a Jenkins slave node for further processing.
* Maven Build: The Jenkins master, running on the master server, triggers a Maven build to create a JAR file for the web application.
* Docker Image Creation: A Docker image is built using the Dockerfile, incorporating the JAR file and other dependencies.
* Docker Hub Push: The Docker image is pushed to Docker Hub, serving as a central repository for Docker images.
* Production Server Deployment: The Jenkins master node establishes an SSH connection with the production server.
* Docker Container Setup: The pipeline pulls the Docker image from Docker Hub and runs a Docker container on the production server.

  
![alt text](https://github.com/PotnuruKumarSunil/multi-branch/blob/dev/EndtoEndPipeline.png)


## Built With
* Jenkins
* Docker
* AWS Cloud
* Httpd Webserver
* Java
* Maven Build tool

## Prerequisites
* Jenkins: Install Jenkins on a master node and configure it to use slave nodes for code execution.<br />
* Jenkins Slave and Maven: Install and Set up Jenkins slave as well as Maven on the slave node to build the web application.<br />
* Docker: Install Docker on the Jenkins slave node and on the production server for image creation and deployment.<br />

## Configuration and Usage
* Clone this repository's Jenkinsfile to your java development environment.
* Make sure you start your jenkins services on the master node and also establish the connection between master and slave and also between master and production environment.
* Make all the required changes, like the IP of the production server and stuff.
* You can now push your code to the repository.

## Conclusion
By implementing this CloudOps pipeline, you can automate the deployment process for your web application, ensuring faster and consistent delivery to the production server. Feel free to customize the pipeline according to your specific requirements and continue enhancing it as your project evolves.

## Contact
Potnuru Kumar Sunil - sunilpotnuru369@gmail.com

Project Link: [https://github.com/PotnuruKumarSunil/end-to-end-pipeline](https://github.com/PotnuruKumarSunil/multi-branch.git)


