## What is the Terraform Work Flow ?

### ===> Write ===> Plan ===> Apply

#### Write => write your terraform code

#### Review => Review the changes that code will make

#### Apply => It will Deploy Actual Infrastructure

### Terraform init (Initialize Directory)

#### Terraform init ==> Initialize The Directory that contain Terraform Code

### Terraform Plan,Apply,Destory

#### Terraform plan ==> Read the Code and Show the Execution Plan for Us it Really help full for Review the Code

#### Terraform apply ==> Deploy the Actual Infrastructure

### Terraform destroy ==> Looks the state file which created during the deployment and destroy the resource

### Terraform code Snippet

```
provider "aws" {
    region = "us-east-1"
}

// create resource

resource "aws_instance" "web" {
    ami = "xxx"
    instance_type = "xxx"
}


// Fetch Resource

data "aws_instance" "my_vm" {
    instance_id = "xxx"
}
```
