# Terraform AWS CI/CD with GitHub Actions

This guide will walk you through setting up a continuous integration and continuous deployment (CI/CD) pipeline for deploying AWS infrastructure using Terraform with GitHub Actions. GitHub Actions allows you to automate your Terraform workflow and securely manage sensitive information like AWS credentials 

## Prerequisites

Before you begin, make sure you have the followingin place:

* GitHub Repository: Create a GitHub repository for your Terraform project.
* Git: Install Git on your local machine. You can download it from Git.
* Terraform Code: Ensure you have your Terraform code in the repository.
* AWS Account: You need an AWS account with an Access Key ID and Secret Access Key.

## Steps
### 1. Clone the Repository

Start by cloning your GitHub repository to your local machine:
```bash
git clone https://github.com/husseinalamutu/githubactions-terraform/
cd githubactions-terraform
```

### 2. Set up Terraform Code
Make sure your Terraform code is organized within the repository directory, properly.

### 3. Edit userdata.tpl
You'll find a file named *userdata.tpl* in your Terraform project directory. This file contains the user data script that will be executed when launching an EC2 instance. Edit the script to include your name. For example:
```bash
#!/bin/bash
sudo apt update -y &&
sudo apt install -y nginx

# Create an HTML file with your desired content
echo "Your Name" > /var/www/html/index.html
```
### 4. Configure GitHub Secrets
To securely manage sensitive information, set up GitHub secrets for the AWS credentials (Access Key ID and Secret Access Key) and your SSH private key. To add a secret, go to your GitHub repository, navigate to "Settings" > "Secrets," and create the following secrets:

* AWS_ACCESS_KEY_ID: Your AWS Access Key ID.
* AWS_SECRET_ACCESS_KEY: Your AWS Secret Access Key.
* AWS_PRIVATE_KEY: Your SSH private key.

With everything set up, each push to the main branch will trigger the GitHub Actions workflow. It will automatically deploy or update your AWS infrastructure using Terraform.

### 5. Cloning the Repo to Your GitHub Account
If you want to use this setup in your own GitHub account, follow these steps:

* Log in to your GitHub account.
* Click the "+" sign in the upper-right corner and choose "New repository."
* Fill in the repository name and other settings.
* In your local environment, set the new repository as the remote origin and push the code:
```bash
git remote set-url origin <new-repo-url>
git push -u origin main
```
You now have your repository with the Terraform code and GitHub Actions workflow in your GitHub account.

### 6. Check Your Website
Check the dns url output from the *terraform apply* command,
![DNS URL](https://github.com/husseinalamutu/githubactions-terraform/assets/94724734/d012ac13-f56b-4583-90a0-5ef6636db525)


if you see your name boldly displayed, congratulations! You now have a CI/CD pipeline for your Terraform AWS project with GitHub Actions.
![The first displayed page](https://github.com/husseinalamutu/githubactions-terraform/assets/94724734/c5252cf9-cc4c-4bed-a74a-92e2b214adb5)
![The main page](https://github.com/husseinalamutu/githubactions-terraform/assets/94724734/38b954e1-76e9-4f4e-b821-25c0ee1d6b32)


PS: Clean up the resources manually: login to your aws console, delete your ec2 instance and the security group created
![TERMINATING INSTANCES](https://github.com/husseinalamutu/githubactions-terraform/assets/94724734/67775bdc-5277-4ef9-bbab-3021fc861221)
Chill for your instance state to fully turn to terminated
![DELETING SECURITY GROUPS](https://github.com/husseinalamutu/githubactions-terraform/assets/94724734/1bbc8795-9b54-4062-accd-738a7ac300b3)

Note also, you can automatically destroy the resources created by terraform by uncommenting the *terraform destroy* in the workflow - main.yaml file.