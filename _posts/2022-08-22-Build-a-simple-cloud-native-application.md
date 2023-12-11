---
layout: post
title: The most popular & common AWS services for Cloud-native application(s)
categories: [AWS,Amazon Web service]
tags: [AWS, Amazon Web service]
---


Let's try to build a cloud native simple application based on most important services from Amazon web services. 

Assume that we are making web-app that requires APIs,Database,etc. In this case, For web-app we are considering the Vue framewark & for the API we are considering the Django( django rest framework) APIs. We can split the application as a Hosting, Domain Routing, API management, Databases, Analytics, Security, Application Orchestration, Monitoring, and AI & ML capabilities etc.

# AWS services we are going to use & discuss: 
#### Static content hosting :
- Amazon S3 
- Cloudfront
- Route 53
#### API hosting :
- Amazon API Gateway
- Application load balancer
- Amazon EC2
- Amazon ECS
#### Database :
- Amazon RDS
- Amazon Aurora
- Amazon Redshift
- Amazon Elasticache
- AWS DynamoDB
#### Application Orchestration :
- Amazon SNS and SQS
- AWS Step Functions
#### Security :

- Amazon VPC , Security Group, Subnet, Internet Gateway 
- AWS Identity Access Management (IAM)
#### Monitoring :
- Amazon CloudWatch
- Amazon Cloudtrail




## Let's start from hosting of a web-app: 
A website that doesn’t involve server-side communication is called a static website.We can deploy any static website easily on Amazon Simple Storage Service (Amazon S3). Amazon S3 basically helps to host javascript files,CSS & HTML files, SVG files, and images all that kind of similar stuff & static assets. 

### Amazon S3: 
AWS S3 stands for Amazon Simple Storage Service is one of the oldest AWS services. It is a cloud-based storage service that can scale to an enormous size and provide high performance, availability, reliability, and security. It is a very cost-effective and secure replacement for your on-premises data center. The data is stored on cloud servers can be accessed through other web applications and websites globally.

After successfully host and store static content on Amazon S3, the next objective is to ensure that my users are going to get optimal performance. At the same time, they access it from anywhere in the world, and to do this, we are using the caching layer service called AWS CloudFront.

### AWS CloudFront :

#### To be continue


