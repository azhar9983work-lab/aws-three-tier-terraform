Our Goal

By the end, we'll have an architecture like this:

                 Internet
                      │
             Application Load Balancer
                      │
        ┌─────────────┴─────────────┐
        │                           │
      EC2                        EC2
      (AZ-A)                    (AZ-B)
        │                           │
        └─────────────┬─────────────┘
                      │
                 RDS MySQL
                (Private Subnets)

CloudWatch
SNS
IAM
Terraform

Everything will be created with Terraform.