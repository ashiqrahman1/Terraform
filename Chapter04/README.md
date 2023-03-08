### Terraform State

- Terradform must store state about your managed infrastructure and configuration, keep track of metadata and improve performance foe the large infrastructure

- By Default State Stored Locally, the file call Terraform.tfstate

- `terraform state` is a command line utility for manipulating and reading the terraform state file

#### Local State vs Remote State

Local State

- Save the Terraform State File locally on your system
- its a defult behaviour

Remote State

- Save State on Remote DataStore optional example, AWS S3, Google Storage

- AllowsSgaring State File Between Distributed Teams

```
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "2.10.0"
    }
  }
  required_version = ">= 0.13"
  backend "s3" {
    profile = "demo"
    region  = "us-east-1"
    key     = "terraform.tfstate"
    bucket  = "terraform-remote-state-file-2023"
  }
}


Saving Terraform State file in S3 Bucket
```
