# Test Portfolio Website on S3

# Overview
This project demonstrates how to deploy a static portfolio website to AWS S3 using GitHub Actions for automated deployment. The workflow ensures that whenever changes are pushed to the main branch, the website is automatically updated on the S3 bucket.

# Key Features
GitHub Actions Workflow: Automates the deployment process when changes are pushed to the repository.
AWS S3 Hosting: Stores and serves the static website.
Live Deployment: Automatic updates through GitHub Actions.

# Project Breakdown

# What are GitHub Actions?
GitHub Actions is a CI/CD (Continuous Integration and Continuous Deployment) tool that enables automation of workflows directly within GitHub repositories. It helps streamline deployment, testing, and build processes.

# Understanding Workflows in GitHub Actions
A workflow is a YAML-based configuration file that defines automated processes triggered by events such as code pushes, pull requests, or manual actions. These workflows consist of jobs, steps, and actions that execute in a defined sequence.

# Workflow Implementation
# Writing the GitHub Actions Workflow
The workflow file (main.yml) defines the process for automatically deploying the website to AWS S3 whenever changes are made to the main branch.

# Setting up AWS with GitHub Actions
The AWS environment is configured using GitHub Secrets to securely store credentials and integrate AWS CLI commands within the GitHub Actions pipeline.

# Live Deployment using Automatic GitHub Actions
The automated workflow ensures seamless deployment, eliminating the need for manual updates. Once code is pushed to the repository, GitHub Actions automatically syncs files to the S3 bucket.

# Deploying the Website on AWS S3
The static website is hosted on an S3 bucket, making it accessible via the assigned S3 URL or a custom domain with CloudFront and Route 53 (optional for enhanced performance and security).

# GitHub Actions Workflow (main.yml)
name: Portfolio Deployment

on:
  push:
    branches:
      - main

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repository
        uses: actions/checkout@v1

      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: eu-west-2

      - name: Deploy Static Site to S3
        run: aws s3 sync . s3://testons3 --delete
# Prerequisites
Before running this project, ensure you have:
✅ An AWS account with an S3 bucket created.
✅ AWS CLI installed and configured locally.
✅ A GitHub repository with GitHub Secrets configured for AWS credentials (AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY).

# Deployment Steps
# Create an S3 Bucket:
Ensure the bucket name matches the one in main.yml (e.g., testons3).
Enable public access (or use CloudFront for better security).

# Set up GitHub Secrets:
Go to GitHub Repository → Settings → Secrets and variables → Actions → New repository secret
Add AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY

# Push Changes to GitHub:
Any updates to the repository will trigger the GitHub Actions workflow, deploying the latest changes to the S3 bucket.

# Future Enhancements
Implement CloudFront for better performance and security.
Add IAM Role-based Authentication for better security.
Enable GitHub Actions artifacts for tracking deployments.

# Conclusion
This project showcases a fully automated deployment pipeline for a static portfolio website hosted on AWS S3 using GitHub Actions. It streamlines updates and ensures the latest changes are reflected live without manual intervention.

