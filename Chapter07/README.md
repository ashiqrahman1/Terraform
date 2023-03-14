#### Terraform fmt,taint,import

- Terraform fmt

  - Formate Terraform Code for Readability
  - Help in keeping code consistent
  - Safe to run at any time
  - command `terraform fmt`

- Terraform taint

  - taint a resource forcing it to be destroyed and re-created
  - Modifies the state file in which cause the recreation work flow
  - command `terraform taint <RESOURCE ADDRESS>`

- Terraform import

  - Map existing Resource to terraform
  - Import same resource to Multiple Terraform Resource can cause unknown behaviour and its not recommended
  - command `terraform import <RESOURCE_ADDRESS.id>`

- Terraform work space
  - Terraform workspace are alternate state files within the same working directory
  - Terraform start with single work space that always called default it cannot be deleted
  - Terraform CLI workspade are assosiate working directory and isolated multiple state file in the same working directory
  - workspace are meant share resource and help enable collaboration
  - access to a workspace name is provided through the ${terraform.workspace} variable

```
resource "aws_instance" "example" {
    count = terraform.workspace == "default" ? 5 : 1  // if the terraform workspace is default the count would be 5 otherwise it will 1
}
```

- Debugging terraform
  - TF_LOG is a environment variable for enabling verbose logging in terraform, by default it will send log to stdrr
  - Can be set the following leve
    - TRACE
    - DEBUG
    - INFO
    - WARN
    - ERROR
  - TRACE is the most verbose levewl of logging and most reliable one
  - to Persist logged output, use the TF_LOG_PATH environment variable
