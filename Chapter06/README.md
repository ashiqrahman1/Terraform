#### Terraform Build in Function

- Terraform Come Pre-packed with function to keep you transform and combine values
- user defined function not allowed in terraform

```
varaible "project-name" {
    type = "string"
    defaults = "prod"
}

resource "aws_vpc" "my_vpc" {
    cidr_block = 10.0.0.0/16
    tags = {
        Name = Join("-",["terraform",var.project-name])
    }
}
```

- Type contrain control the type of variable values

##### primitive

Single Type Values

- number
- string
- boolean

##### Complex

Multiple Type Values

- List
- Tuple
- Map
- Object

- `Collection` Type Allows Multiple Values of one primitive type to be grouped together
- contruction of these collection include

  - list
  - map

- `Structural` Type Allow Multiple Values of different Primitive Type to be grouped together
- It Includes

  - object
  - tuple

- `Dynamic` Type the `Any` Contrain
- `any` is a placeholder for a primitive type yet to decided
- Actual Type will be determined at run time

##### Terraform Dynamic Block

- Dynamic Contructs Repeatable Tasks Configuration block inside terraform resource
- Support Within Following Type
  - resource
  - data
  - provider
  - provisioner

```
resource "aws_security_group" "my_sg" {
    name = "my_security_group"
    vpc_id = aws_vpc.my_vpc.id
    ingress {
        from_port = 21
        to_port = 22
        protocol = tcp
        cidr_block = ["0.0.0.0/0"]
    }
    ingress {
        ------
        ------
    }
}


with dynamic blocks
resource "aws_security_group" "my_sg"{
    name = "my_security_group"
    vpc_id = aws_vpc.my_vpc.id
    dynamic ingress {
        for_each = var.rules
        content {
            from_port = ingress.value['port']
            to_port = ingress.value['port']
            protocol = ingress.values['proto']
            cidr_block = ingress.values['cider']
        }
    }
}


variable "rules" {
    default = [
        {
            port = 22
            proto = "tcp"
            cidr_block = ["0.0.0.0/0"]
        },{
            port = 80
            proto = "tcp"
            cidr_block = ["0.0.0.0/0"]
        }
    ]
}

- Dynamic Block expect a complex variable type to itrate over
- it acts like a for loop and output a nested block each element in your variable
```
