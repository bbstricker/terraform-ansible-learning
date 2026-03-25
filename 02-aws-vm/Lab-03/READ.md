# Lab 02 — Terraform with AWS

## What I Learned
- Providers
- Resources
- Variables
- Creating AWS Dynamo DB with Terraform
- Adding Dynamo DB table item
- Using S3 bucket policy to define access

## Code main.tf

resource "aws_dynamodb_table" "cars" {
  name           = "cars"
  hash_key       = "VIN"
  billing_mode   = "PAY_PER_REQUEST"
  attribute {
    name = "VIN"
    type = "S"
  }
}

resource "aws_dynamodb_table_item" "car-items" {
  table_name = aws_dynamodb_table.cars.name
  hash_key   = aws_dynamodb_table.cars.hash_key
  item = <<EOF
  {
      "Manufacturer": {"S": "Toyota"},
      "Make": {"S": "Toyota"},
      "Year": {"N": "2004"},
      "VIN": {"N": "4Y1SL58448Z4114391"}
  }
EOF
}





#----------------------------------------------------------------
## What Broke / How I Fixed It
- Missing AWS Dynamo DB
- Dynamo DB table and item

## Real-World Insight
- 
- 


