#### Terraform Modules

- A Moddule is the container for multiple resource that are used together
- Every Terraform Configuration has at least one Module Called `root` Module,Which Consist of your code file in your main working directory

- your can reference module from
  - public registry
  - private registry

```
module "module_name" {
    source = "./module_source"
    version = "xxx"
    region = "us-east-1"
}
```

```
module example for aws vpc

module/vpc
    - main.tf
    - variables.tf
    - outputs.tf

main.tf
-------
provider "aws" {
  region = var.region
}

resource "aws_vpc" "my_vpc" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "my_subnet" {
  vpc_id     = aws_vpc.my_vpc.id
  cidr_block = "10.0.1.0/24"
}

data "aws_ssm_parameter" "ami" {
  name = "/aws/service/ami-amazon-linux-latest/amzn2-ami-hvm-x86_64-gp2"
}

variables.tf
------------
variable "region" {
  type    = string
  default = "us-east-1"
}

outputs.tf
----------
output "subnet_id" {
  value = aws_subnet.my_subnet.id
}

output "ami_id" {
  value = data.aws_ssm_parameter.ami.value
}
```
