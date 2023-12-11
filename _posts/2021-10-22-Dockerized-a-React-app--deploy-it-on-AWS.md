---
layout: post
title: Deploy React App to AWS ECS for Production
categories: [AWS, deployment, react,Docker]
tags: [python]
---


Today, I will talk about how to dockerize a react app, then deploy it on AWS by using AWS ECR & Fargate. 
To Deploy React App to AWS ECS for Production, we need to follow below steps:
Firstly, We need to Dockerize React app.
Then we need to build the container image and push it to ECR.
After that we need to create an ECS Cluster.
Create a Task within the cluster.
Create service within the cluster to run the Task
Prerequisite : 
Create a new react app
This is only required if you are starting from scratch and don't have an existing code/app that you would like to containerize.
$ npx create-react-app my-app
Docker install
$ sudo apt-get update
$ sudo apt-get install docker-ce docker-ce-cli containerd.io
NGINX:
$  sudo apt-get update
$  sudo apt-get install nginx
AWS CLI
For the latest aws cli 
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
Version check : 
$ aws --v
No alt text provided for this image
Make sure , it’s AWS CLI 2 
Configuration: 
We need to create conf. files for 
1. Nginx (our web server)
2. Docker file (to build the Docker image)
Docker  
What is Docker?
Docker helps us to make containerized apps. What that means is that we create a single package that not only contains the code of our app but also all the required Libraries, software, configurations, etc.
So, let’s first create a Docker-file in the root folder of react project.
No alt text provided for this image
Inside your app directory create a new file and Inside that file write the following lines of code. So, on docker we took images like node & nginx. 
Nginx Conf
worker_processes  1;

events {
  worker_connections  1024;
}

http {
  server {
    listen 80;
    server_name  localhost;

    root   /usr/share/nginx/html;
    index  index.html index.htm;
    include /etc/nginx/mime.types;

    gzip on;
    gzip_min_length 1000;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;

    location / {
      try_files $uri $uri/ /index.html;
    }
  }
}
Dockerfile
FROM node:lts-alpine as build 

WORKDIR /app

COPY package.json .
RUN npm install 
COPY . .
RUN npm run build

FROM nginx
COPY ./nginx/nginx.conf /etc/nginx/nginx.conf 

COPY --from=build /app/build /usr/share/nginx/html 

Here is the source code, you can clone & practice on hands-on.
Then we need to build docker by using command:
$ sudo docker build -t app .
After build the dockerfile, let’s run it by using command:
$ docker run -p 80:80 appname 
Now, you can check locally on port 80.
What is ECS?
Amazon Elastic Container Service (Amazon ECS) is a service provided by AWS to orchestrate containers. In layman's terms, consider it as a service that is specifically tailored to move your containerized applications to production.
How to build the container image and push it to ECR : 
Firstly , we need to configure the aws by using aws cli.
To configure aws with cli , we need AWSAccessKeyId & security key. You can get Access Key ID and Secret Access Key from IAM.
No alt text provided for this image

$ aws configure 
No alt text provided for this image

After configuring Aws cli, we need to go to ECR to create a Repository. 
Creating an ECR repository 
No alt text provided for this image
To login with AWS ECR: 
$ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin xxxxxxxxxx.dkr.ecr.us-east-1.amazonaws.com
No alt text provided for this image

Creating an ECS Cluster: 
Now go to the services console, type ECS and select it.
Click on Create Cluster.
Select Networking only from Select Cluster Template and then click Next Step.
Provide a cluster name under configure cluster and click on CreateVpc. You can also select an existing Vpc.
Click Create.
After successfully creating it click on view cluster.
ECS
Once our container image has been pushed, we are now ready to use ECS and all the awesomeness it has to offer. Head over to Amazon Elastic Container Service (Amazon ECS) and create a cluster.
Select "Network Only" and click "Next Step".
No alt text provided for this image
Give whatever name you would like (but remember it), select "create VPC", click "create".
*Note: You can also choose an existing VPC.
No alt text provided for this image


No alt text provided for this image
Once the Cluster has been created, select 'View Cluster'.
No alt text provided for this image

Select "Task Definitions" from the left sidebar.
No alt text provided for this image
No alt text provided for this image
Now we need to add a container of the image we pushed to ECR earlier. Give a name to container and copy-paste the image URI (can be copied from ECR repositories list). Enter "80" in the port mapping field. Click "Add".
No alt text provided for this image
Once the container is added, click "Create" to finish Task creation.
Go inside the cluster we have created. In the "Services" tab, click "Create".
No alt text provided for this image
Select "Fargate" as the launch type. Select the task definition we created above (my-app-task in my case), select revision as 1 (latest). Select "LATEST" in platform version, choose the cluster we created in "Cluster". Give a name to your service. Enter "1" in the "Number of tasks" field. Click "Next step".
No alt text provided for this image
No alt text provided for this image
After clicking next a review page will comes up
No alt text provided for this image

After creating service , we can check our deployment by using public IP from clusters tasks.
No alt text provided for this image
So, Our public IP is http://3.87.231.104/
No alt text provided for this image

Instead of public IP, you can add DNS to an Elastic Load Balancer (ELB).

Thank you for your time.
Regards
TANVIR AHMED