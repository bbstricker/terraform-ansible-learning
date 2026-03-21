# Lab 01 — Terraform with AWS

## What I Learned
- Providers
- Resources
- Variables
- Terraform with AWS:
* Create Users with IAM role and added needed permissions

## Code main.tf

resource "aws_iam_user" "admin_user" {
  name = "lucy"
  tags = {
    Description = "Technical Team Leader"
  }
}


provider "aws" {
  region = "us-east-2"
}


resource "aws_iam_policy" "adminUser" {
  name = "AdminUsers"
  policy = <<EOF
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
	             "Action": "*",
	             "Resource": "*"
	         }      
       ]
   }
  EOF
}

resource "aws_iam_user_policy_attachment" "lucy-admin-access" {
  user = aws_iam_user.admin_user.name
  policy_arn = aws_iam_policy.adminUser.arn

}


#----------------------------------------------------------------
## What Broke / How I Fixed It
- AWS credentials issue
- Missing region variable
- AWS IAM Policy Attachment

## Real-World Insight
- Verifying access and secret Keys
- Need to verify AWS policy json for IAM role attachment

