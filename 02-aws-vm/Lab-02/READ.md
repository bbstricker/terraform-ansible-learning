# Lab 02 — Terraform with AWS

## What I Learned
- Providers
- Resources
- Variables
- Creating AWS S3 Bucket with Terraform
- Adding objects to the S3 bucket
- Using S3 bucket policy to define access

## Code main.tf

resource "aws_s3_bucket" "finance" {
  bucket = "finance-21092020"
  tags = {
    Description = "Finance and Payroll"
  }
}


resource "aws_s3_bucket_object" "finance-2020" {
  bucket = "aws_s3_bucket.finance.id"
  key    = "finance-2020.doc"
  content = "/root/fiance/finance02020.doc"
}

data "aws_iam_grouo" "fainace-data" {
  group_name = "fiance-analysts"
}

resource "aws_s3_bucket_policy" "fiance-policy" {
  bucket = aws_s3_bucke.fiance.id
  policy = <<EOF                                           #Read-object.json policy sample
  {
     
          "Version": "2012-10-17"
          "Statement": [
              {
	          "Action": "*",
                  "Effect": "Allow",
	          "Resource": "arn:aws:s3:::${aws_s3_bucket.finance.id/*",
	          "Principal": {
		     "AWS": [
		        "${data.aws_iam_group.finance-data.arn}"
		     ]
	          }
	      }
           ]

  }
EOF
}









#----------------------------------------------------------------
## What Broke / How I Fixed It
- Missing AWS S3 Bucket Policy
- 

## Real-World Insight
- Verifying S3 Bucket
- Need to verify AWS Bucket policy json for  attachment

