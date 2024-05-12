---
layout: post
title: "AWS Cloud Resume Challenge"
subtitle: "A Weekend Personal Project"
categories: ["AWS", "Lambda", "IaC", "CI/CD"]
tags:
  - AWS
  - Automation
  - Serverless
  - Cloud
  - Resume 
  - Challenge 
  - Terraform 
  - GitHub Actions 
  - Lambda 
  - S3 
  - CloudFront 
  - Route 53,
  - DynamoDB
  - API Gateway
---

The AWS Cloud Resume Challenge is a project that has been gaining popularity among cloud enthusiasts. The challenge involves creating a simple resume website and deploying it using various AWS services. In this blog post, we will walk through how I completed the AWS Cloud Resume Challenge over a weekend project.

## The Journey:
As a cloud enthusiast, I was excited to take on the AWS Cloud Resume Challenge. The challenge involves creating a simple resume website using HTML, CSS, and JavaScript. The website should display my resume information and include a visitor counter that increments every time someone visits the site. More details about the challenge can be found [here](https://cloudresumechallenge.dev/).

In addition to the website, I needed to create a RESTful API that would return my resume data in JSON format. The API should also have a route that returns the visitor count, which would be stored in a DynamoDB table.

Original challenge requires the lambda to be created in python, but I decided to use .net core as I'm more interested in that.
Also, I used Terraform to deploy the resources and GitHub Actions for CI/CD pipelines, these are additional requirements that I added to the challenge.

## High-Level Architecture:
Here is the high-level architecture of the project:

![Architecture Diagram]({{site.baseurl}}/img/aws_cloud_resume_challenge.png){: .center-image }

1. **Static Website**: The resume website is hosted as a static website on Amazon S3 and distributed using Amazon CloudFront for faster content delivery.
2. **Custom Domain**: I configured a custom subdomain using Amazon Route 53 to point to the CloudFront distribution.
3. **Lambda Functions**: The RESTful API is implemented using AWS Lambda functions. The Lambda functions are written in .NET Core and are deployed behind an API Gateway.
4. **DynamoDB**: The visitor count is stored in an Amazon DynamoDB table. The Lambda function increments the count every time the website is visited.
5. **Terraform**: I used Terraform to define and deploy the AWS resources. The Terraform code is stored in a GitHub private repository and state is stored in an S3 bucket.
6. **GitHub Actions**: I set up CI/CD pipelines using GitHub Actions to automate the deployment process. The pipelines build and deploy the Lambda functions and update the website whenever changes are pushed to the repository.

## Why I Took on the Challenge:

Even though I have professional experience with AWS services, I wanted to take on the challenge as a personal project to learn new things and experiment with different technologies. The challenge provided a structured way to build a project from scratch and deploy it using AWS services. It also allowed me to practice using Terraform and GitHub Actions for infrastructure as code and CI/CD pipelines.

## Takeaways:
This project taught me the importance of planning and architecture when building complex systems. It also showed me how to effectively use Terraform to deploy resources and manage infrastructure as code. The CI/CD pipelines using GitHub Actions helped automate the deployment process and ensure that changes were deployed quickly and efficiently.

For those looking to take on similar challenges, I recommend experimenting with different AWS services and technologies to find what works best for you. And, of course, don't forget to have fun!

My cloud resume project is now live at [https://myawsresume.seshuk.com/](https://myawsresume.seshuk.com/). Feel free to check it out and let me know your thoughts!