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
- Allow CodeBuild to CodePipeline, etc.
Create Build Project → Ready for integration with CodePipeline

### Adding Correct Requirements File Path in Buildspec
- Make sure you provide the exact path to your requirements.txt inside the buildspec.yml.

### IAM Role Creation for CodeBuild

Create an IAM role that provides the required permissions for AWS CodeBuild.  
Name the role: **`code-build-service-role`**

#### **Steps**
1. Navigate to **IAM → Roles → Create Role**
2. Choose **AWS Service** → Select **CodeBuild**
3. Attach the following policies:
   - **AWSCodeBuildDeveloperAccess**
   - **CodePipelineFullAccess** (if used with pipelines)
4. Set the role name as: **`code-build-service-role`**
5. Create the role and attach it to your CodeBuild project.

This role allows CodeBuild to CodePipeline, and other required services during the build process.

### AWS Systems Manager Parameter Store

AWS Systems Manager (SSM) Parameter Store is a secure and scalable service used to store configuration data and secrets.  
It helps you manage sensitive values (like passwords, tokens, and URLs) without hardcoding them in your code or build files.

---

### Adding Parameters (Standard Tier – SecureString)

Store your Docker credentials and registry URL in **SSM Parameter Store** using **Standard Tier** and **SecureString** for encryption.

Create the following parameters:

| Parameter Name                                   | Type          | Value                 |
|--------------------------------------------------|---------------|------------------------|
| `/myapp/docker-credentials/password`             | SecureString  | *docker password*      |
| `/myapp/docker-credentials/username`             | SecureString  | *docker username*      |
| `/myapp/docker-registry/url`                     | SecureString  | `docker.io`            |

#### **Steps**
1. Go to **AWS Systems Manager → Parameter Store → Create Parameter**
2. Select:
   - **Tier:** Standard  
   - **Type:** SecureString  
3. Enter the parameter name (e.g., `/myapp/docker-credentials/password`)
4. Add the corresponding value
5. Create the parameter
6. Repeat for all parameters listed above

These parameters can now be safely accessed within your CodeBuild project or CodePipeline using the AWS SDK or environment variables.

To create a build in AWS CodeBuild, navigate to your project in the AWS Console and click **Start Build**, or use the AWS CLI with `aws codebuild start-build --project-name my-codebuild-project`. Once the build starts, you can check its status in the **Build history** of the console or via CLI using `aws codebuild batch-get-builds --ids <build-id>`. Look for the `"buildStatus"` field—`SUCCEEDED` indicates the build completed successfully, while `FAILED`, `FAULT`, or `STOPPED` indicates an issue. 




