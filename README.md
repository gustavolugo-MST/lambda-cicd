# Project name: lambda-cicd

!Architecture

## The problem
All enterprises have a common challenge, system bugs quickly can disable or break a business site. More specifically, it's software engineers that need to deal with these software bugs that can create havoc in day to day business operations. Instead of deploying new code manually, where a simple typo or nesting issue creates a new bug, a github actions workflow automates the (CICD) Continuous Integration and Continuous Deployment Process and verifies code at a pull request. This automation alerts software engineers to correct bugs before deployment can happen.

## What I built
I built a two github workflows. The first validates an AWS Cloudformation template, builds a temporary stack with an S3 Bucket on pull request and then the push workflow updates the Lambda funciton code on push request. The continues integration, during pull request,  and continuous deployment, during push request,  provides an efficient CICD process. Finally, the S3 bucket that was created for this test environment is deleted on merge.

## Decisions I made
- I choose lambda for cost and efficiency. AWS Lambda only works when its enabled and that saves an organization money. This is way more efficient than having a dedicated server running 24 hours a day. 
- I choose AWS Cloudformation because it serves as a code template. Build it once and it can redeploy every time its needed. Again efficiency is key.
- We are in an AWS environment so these services make sense. 

## What broke and how I fixed it
I made a nesting mistake. AWS reads code in a very specific way. Once i indented a bit more my instructions were in line with how aws reads code. That fix enabled aws to deploy a S3 Bucket that was attached to this project. 

## Result
What this architecture does now versus what a manual version would do is automate the process. So instead of uploading code to AWS to correct a bug, the github actions workflow now checks the code on pull request to validate the code efficacy then once it shows that it is written correctly, it will upload to the AWS stack and deploy. This is a massive advancement from manually uploaded code without testing it to later find out that something was wrong. You added another bug and now the site is additionally not working well. 

## How to run it
```bash
git clone https://github.com/[you]/[repo].git
cd [repo]
terraform init && terraform apply
