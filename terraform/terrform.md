# IAAS (Infrastructure as a code)
Automating infrastructure provisinioning to deploy environment faster and in a consistent fashion. It offers on-demand infrastructure resources, such as compute, storage, networking, and virtualization, to businesses and individuals via the cloud.

## Terraform 
HashiCorp Terraform is an infrastructure as code tool that lets you define both cloud and on-prem resources in human-readable configuration files that you can version, reuse, and share.
The core Terraform workflow consists of three stages:

+ Write: You define resources, which may be across multiple cloud providers and services. For example, you might create a configuration to deploy an application on virtual machines in a Virtual Private Cloud (VPC) network with security groups and a load balancer.
+ Plan: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration.
+ Apply: On approval, Terraform performs the proposed operations in the correct order, respecting any resource dependencies. For example, if you update the properties of a VPC and change the number of virtual machines in that VPC, Terraform will recreate the VPC before scaling the virtual machines.

<img src="https://developer.hashicorp.com/_next/image?url=https%3A%2F%2Fcontent.hashicorp.com%2Fapi%2Fassets%3Fproduct%3Dterraform%26version%3Dv1.4.6%26asset%3Dwebsite%252Fimg%252Fdocs%252Fintro-terraform-workflow.png%26width%3D2038%26height%3D1773&w=2048&q=75" width="520">
