# Week 0 — Billing and Architecture

# Update our gitpod.yml to include the following task
tasks:
  - name: aws-cli
    env:
      AWS_CLI_AUTO_PROMPT: on-partial
    init: |
      cd /workspace
      curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
      unzip awscliv2.zip
      sudo ./aws/install
      cd $THEIA_WORKSPACE_ROOT

# user create with admin role
Go to IAM Users Console create a new user
Enable console access for the user
Create a new Admin Group and apply AdministratorAccess
Create the user and go find and click into the user
Click on Security Credentials and Create Access Key
Choose AWS CLI Access

# Set Env Vars
export AWS_ACCESS_KEY_ID=""
export AWS_SECRET_ACCESS_KEY=""
export AWS_DEFAULT_REGION=us-east-1

# gitpod env vars
gp env AWS_ACCESS_KEY_ID=""
gp env AWS_SECRET_ACCESS_KEY=""
gp env AWS_DEFAULT_REGION=us-east-1

# Check that the AWS CLI is working and you are the expected user
aws sts get-caller-identity
