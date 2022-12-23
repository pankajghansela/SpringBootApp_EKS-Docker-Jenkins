# Containerize a demo Springboot microservices app with Docker and deploy into Amazon EKS Cluster using Jenkins Pipeline and Kubectl CLI Plug-in

Overall Workflow: (A schematic representation available in "Overall_Architecture.jpg")

	1. A Dockerfile to run the containerized version of the springboot app and 

	2. Code commit to the GitHub repo

	3. Initialize an EKS cluster (2 worker nodes used)

 	4. Create a Jenkins server (used an EC2 instance) and install Docker, Maven, Kubectl CLI plugins and add credentials from the KubeConfig file

	5. Create the Jenkinsfile with the declarative pipeline with diff. stages (elaborated below)


The Jenkins pipeline contains the following stages:

	- Git checkout: Clone the git repository

	- Build: Build the .jar files for the demo app

	- Docker image: Build the docker image from the Dockerfile

	- Push image: Push the created Docker image to the designated private repo in the AWS ECR

	- Kubernetes deploy: Deploy the app on Kubernetes based on the "eks-deployment.yaml" file, pulling the Docker image from ECR 


------------------------------------------------------------------------

The demo springboot app is just a simple sign-up page to enter your name and get a list of all the names entered


Please note that all the AWS services created: EC2 instance, private ECR repo and the EKS cluster were created only for the purposes of this project and have since been disabled


