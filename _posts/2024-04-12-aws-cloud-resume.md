---
layout: post
title: "Elevating the AWS Cloud Resume Challenge"
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

As an experienced AWS solutions architect, I recently undertook the AWS Cloud Resume Challenge to demonstrate advanced cloud architecture principles and showcase my expertise in a compact, innovative project. While the challenge is often used as a learning tool for beginners, I saw it as an opportunity to push the boundaries and implement best practices in cloud infrastructure.

## Why I Took on the Challenge:

Even though I have professional experience with AWS services, I wanted to take on the challenge as a personal project to learn new things and experiment with different technologies. The challenge provided a structured way to build a project from scratch and deploy it using AWS services. It also allowed me to practice using Terraform and GitHub Actions for infrastructure as code and CI/CD pipelines.

## The Project Overview
The AWS Cloud Resume Challenge typically involves creating a resume website and deploying it using various AWS services. However, I decided to elevate the challenge by incorporating advanced techniques and technologies that reflect real-world enterprise scenarios. More details about the challenge can be found [here](https://cloudresumechallenge.dev/).

## Enhancing the Standard Challenge

My implementation went beyond the basic requirements

## High-Level Architecture:
Here is the high-level architecture of the project:

![Architecture Diagram]({{site.baseurl}}/img/aws_cloud_resume_challenge.png){: .center-image }

1. Frontend: Developed a responsive resume website using HTML, CSS, and JavaScript, with a focus on performance optimization and accessibility.
2. Backend: Instead of the suggested Python, I chose to implement the Lambda function in .NET Core, showcasing my versatility in cloud-native development.
3. Infrastructure as Code: Utilized Terraform for infrastructure provisioning, ensuring reproducibility and version control of the entire AWS environment.
4. CI/CD Pipeline: Implemented a robust CI/CD pipeline using GitHub Actions, demonstrating DevOps best practices for continuous deployment and integration.
5. API Development: Created a RESTful API that serves the resume data in JSON format and manages a visitor counter, illustrating microservices architecture principles.
6. Database: Leveraged DynamoDB for storing visitor counts, showcasing my expertise in NoSQL database design and management in serverless architectures.

By approaching this project from an expert's perspective, I was able to transform a straightforward challenge into a comprehensive demonstration of cloud architecture, DevOps practices, and software engineering principles. This weekend project serves as a testament to how seasoned professionals can use seemingly simple tasks to showcase advanced skills and innovative approaches in cloud computing.

## Takeaways:
This project taught me the importance of planning and architecture when building complex systems. It also showed me how to effectively use Terraform to deploy resources and manage infrastructure as code. The CI/CD pipelines using GitHub Actions helped automate the deployment process and ensure that changes were deployed quickly and efficiently.

For those looking to take on similar challenges, I recommend experimenting with different AWS services and technologies to find what works best for you. And, of course, don't forget to have fun!

My cloud resume project is now live at [https://myawsresume.seshuk.com/](https://myawsresume.seshuk.com/). Feel free to check it out and let me know your thoughts!
