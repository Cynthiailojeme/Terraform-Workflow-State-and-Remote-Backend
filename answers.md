**1. What is the Terraform state file used for?**
   It tracks all real-world resources Terraform has created and maps them
   to your configuration. It lets Terraform know what already exists so
   it only makes the changes needed on the next run.

**2. Why is storing state locally risky in a team environment?**
   Team members cannot share or sync local state files. Two people running
   Terraform at the same time could corrupt the state or create duplicate
   resources. There is also no locking mechanism to prevent conflicts.

**3. What is a remote backend?**
   A remote backend stores the state file in a shared location such as an
   S3 bucket so the whole team reads from and writes to the same state.
   It also supports state locking (via DynamoDB) to prevent two people
   from applying changes at the same time.

**4. Example S3 remote backend configuration block:**

   terraform {
     backend "s3" {
       bucket = "my-terraform-state-bucket"
       key    = "project/terraform.tfstate"
       region = "us-east-1"
     }
   }

   Note: Using this backend requires valid AWS credentials. In a real
   project, credentials would be configured via AWS CLI (aws configure)
   or environment variables before running terraform init.
