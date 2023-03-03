# Chapter 03

### Terraform Provider

- Provider are the way toabstract intergration with API LAyer of infrastructure Vendors

- Terraform by Default, Looks the Provider from Terraform Provider Registry

- Terraform Install Provider when initializing the working Directory

### Terraform State

- A way for Terraform to Keep Track on waht changes has been Deployed

- Help the Terraform to Calculate Deployment Delta and Create new deployment Plans

```
Terraform Variable and Output


variable "image_id" {
  type = string
}

variable "availability_zone_names" {
  type    = list(string)
  default = ["us-west-1a"]
}

variable "docker_ports" {
  type = list(object({
    internal = number
    external = number
    protocol = string
  }))
  default = [
    {
      internal = 8300
      external = 8300
      protocol = "tcp"
    }
  ]
}


Reference the variable

var.image_id
```

### Terraform Output

- Output put Value are like return value that you want to track after a successfull deployment

```
output "instance_ip_addr" {
  value = aws_instance.server.private_ip
}

```

### Terraform Provisioner

- Terraform way of bootstrapping custome script, command or action

- it can run either locally or remotely

- within the Terraform code, each individual resource can have there own "Provisioner"

- There are Two Type of Provisioner create time and destroy time Provisioner

- Terraform cannot track the changes to Provisioner

```
resource "null_resource" "null" {
    provisioner "local-exec" {
        command = "echo '0' > status.txt"
    }

    provisioner "local-exec" {
        when = destroy
        command = "echo '1' > status.txt"
    }
}
```
