#AWS-End-to-End-CI
## 🌟 Introduction
This project showcases a fully automated AWS Continuous Integration (CI) pipeline built using CodePipeline, CodeBuild, IAM, and Systems Manager (SSM). It delivers a clean, scalable, and secure workflow that builds, tests, and packages your application with zero manual effort.

## 💡 Why It Matters
- Ensures consistent, reliable builds every time
- Eliminates manual errors with automation-first workflows
- Protects sensitive data using SSM-managed secrets
- Improves development speed with fast, repeatable CI cycles
- Enables teams to ship confidently with AWS-native security & scalability

## 🌟 Overview
This project demonstrates a complete Continuous Integration (CI) setup on AWS using:

- AWS CodePipeline – Orchestrates the entire CI flow
- AWS CodeBuild – Builds, tests, packages artifacts
- IAM Role for CodeBuild – Secure, least-privilege access
- AWS Systems Manager (Parameter Store + Session Manager) – Secret management & debuggin

✨ 100% AWS-managed, scalable, secure, and production-ready.

## 🏗️ Architecture Diagram
![Architecture Diagram](./architecture.png)

## AWS CodeBuild 🚀

AWS CodeBuild is a fully managed continuous integration (CI) service that compiles your source code, runs tests, and produces build artifacts. You don’t need to manage servers or build environments—CodeBuild automatically scales and processes multiple builds in parallel.

### Creating a CodeBuild Project (Short Steps)

1. Open AWS CodeBuild → Click Create build project
2. Connect Source Provider → Choose GitHub →
- Authorize your GitHub account
- Select the repository you want to build
3. Choose Environment →
- Environment image: Managed image
- Operating System: Ubuntu
- Runtime: Standard
4. Specify Buildspec →
- Use a buildspec.yml file from your repo
5. Configure Service Role (IAM) →
- Allow CodeBuild to access S3, CloudWatch Logs, CodePipeline, etc.
Create Build Project → Ready for integration with CodePipeline


