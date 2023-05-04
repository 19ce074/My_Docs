# IAAS (Infrastructure as a code)
Automating infrastructure provisinioning to deploy environment faster and in a consistent fashion. It offers on-demand infrastructure resources, such as compute, storage, networking, and virtualization, to businesses and individuals via the cloud.

## Terraform 
HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share.

The core Terraform workflow has three steps:

+ Write - Author infrastructure as code.
+ Plan - Preview changes before applying.
+ Apply - Provision reproducible infrastructure.



<img src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Dv1.4.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=2048&q=75" width="520">

### Installation
Go to the official installtion documentation (https://developer.hashicorp.com/terraform/downloads)

### Creating a sample resource

```
resource "local_file" "pet" {
  filename = "/home/vivek/Projects/pets.txt"
  content = "We love pets!"
}
```
+ "local" is provider </br>
+ "file" is file type </br>
+ "pet" is resource name </br>

With the configuration file ready, we can create file resource using the terraform command. 
1) Run the `terraform init` command. To check the config file and initialize the working dir where the .tf file is located.
2) Run the `terraform plan` command. It will show the actions that will be carried out.
3) Run the `terraform apply` command to execute and create the resource.
4) Run the `terraform show` command to see the details of the resource that we created.
5) Run the `terraform destroy` command to destroy the resource.

### Input Variables
Input variables let you customize aspects of Terraform modules without altering the module's own source code. 
In normal convection we create a variable.tf file to declare and store variables. We then access the variable from the variable.tf file from the main.tf file.

#### Main.tf 
```
resource "local_file" "pet" {
	filename = var.filename
	content = var.content
}
```

#### Variable.tf
```
variable "filename" {
	type = string
	default = "/home/vivek/Projects/pets.txt"
}

variable "content" {
	default = "We love pets !!"
}
```
