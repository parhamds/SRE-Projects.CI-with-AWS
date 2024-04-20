# Project Overview: CI with AWS Resources

This project automates the Continuous Integration (CI) process using various AWS services. Below is an overview of the steps involved:

## Overview

- **Code Repository Migration:** Transfer the repository from GitHub to AWS CodeCommit.
- **Artifact Repository Creation:** Establish a CodeArtifact repository for managing dependencies.
- **Dependency Management:** Modify Java code to utilize CodeArtifact as the repository for dependencies.
- **Pipeline Setup:** Configure a CI pipeline triggered by code pushes, utilizing CloudWatch Events.
- **Code Analysis:** Utilize SonarQube for code analysis.
- **Build Process:** Employ AWS CodeBuild for building the code.
- **Artifact Storage:** Store the final artifact on an S3 bucket.
- **Notification System:** Send notifications via email using SNS topics.

## Detailed Steps

1. **Repository Migration:**
   - Transfer the repository from GitHub to AWS CodeCommit.

2. **Artifact Repository Creation:**
   - Create a CodeArtifact repository.
   - Adapt Java code to use CodeArtifact as the dependency repository.

3. **Configuration Setup:**
   - Create a `buildspec.yaml` file.
   - Set up a SonarCloud account, generating a token, creating a new organization, and project.
   - Store SonarQube credentials in AWS Systems Manager Parameter Store.
   - Configure `buildspec.yml` to read credentials from Parameter Store.

4. **AWS Service Permissions:**
   - Create IAM policy for accessing Systems Manager.
   - Modify service roles for CodeCommit and CodeBuild to grant access to Parameter Store.
   - Attach `codeartifactreadonlyaccess` policy to service roles.

5. **AWS Resource Creation:**
   - Establish CodeBuild projects for SonarQube analysis and code building.
   - Create an S3 bucket for storing artifacts.
   - Set up an SNS topic and subscription for email notifications.

6. **Pipeline Creation:**
   - Design pipeline stages including source code retrieval from CodeCommit, code analysis via SonarQube, code building with CodeBuild, and artifact storage on S3.
   - Configure notification rules to send alerts to the SNS topic.

## Code Structure

- **vprofile-project:**
  - `ci-aws/aws-files`: Contains necessary configuration files and scripts for CI setup.

## Usage

- Developers push code changes triggering the CI pipeline.
- CloudWatch Events detect code pushes initiating the pipeline.
- SonarQube analyzes the code.
- CodeBuild builds the code and manages dependencies.
- Final artifacts are stored in the designated S3 bucket.
- Email notifications are sent via SNS topic.

## Dependencies

- AWS services: CodeCommit, CodeArtifact, CloudWatch Events, CodeBuild, S3, SNS.
- SonarQube for code analysis.
