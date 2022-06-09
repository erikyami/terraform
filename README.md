# terraform

Estudos Terraform

Material de Estudos:

https://learn.hashicorp.com/collections/terraform/certification-associate-tutorials

https://www.terraform.io/intro

## Benefits:
 - Automate Software Defined Networking
 - Interacts and takes care of communication with control layer APIs with ease
 - Supports a vast array of private and public cloud vendors
 - Tracks state of each resource deployed.

 ## Terraform Workflow

  - Write [Write your Terraform code]
    - This would generally start off with creating a GitHub repo as a common best practice.
  - Plan [Review]
    - You'll continually add and review changes to code in your project
  - Apply [Deploy]
    - After one last review/plan, you'll be ready to provision real infrastructure


### Terraform Init [Initializing the Working Directory]
`terraform init`

- Initializes the working directory that contains your Terraform code
    - Dowloads ancillary components
        - downloads modules and plugins
    Sets up backend
        - Sets up the backend for storing Terraform state file, a mechanism by which Terraform tracks resources.


### Terraform Key Concepts: Plan, Apply, and Destroy

- Terrafom Plan
    - Reads the code and then creates and shows a "plan" of execution/deployment
    - This command does not deploy anything. Consider this a read-only command.
    - Allows the user to "review" the action plan before executing anything
    - At this stage, authetication credentials are used to connect to your infrastructure, if required.

- Terraform Apply
    - Deploys the instructions and statements in the code
    - Updates the deployment state tracking mechanism file, a.k.a "state file"

- Terraform Deployment: Terraform Destroy
    - Looks at the recorded, stored state file created during deployment and destroys all resources created by your code
    - Should be used with caution, as it is a non-reversible command. Take backups, and be sure that you want to delete infrastructure.

### Resource Addressing in Terraform: Understanding Terraform Code
- Terraform Code Snippet (Cofiguring the Provider)

Providers
    
```
    provider "aws" {
        region = "us-east-1"
    }
```    

```
    provider "google" {
        credentials = file("credentials.json")
        project     = "my-gcp-project"
        region      = "us-west-1"
    }
```  

Resources
```
    resource "aws_instance" "web" {
        ami             = "ami-a1b2c3d4"
        instance_type   = "t2.micro"
    }
```  
Resource Address -> aws_instance.web

Data Source
```
    data "aws_instance" "my-vm" {
        instance_id = "i-1234567890abcdef0"
    }
```
Resource Address -> data.aws_instance.my-vm


- Terraform executes code in file with the .tf extension
- Initially, Terraform looks for providers in the Terraform providers registry [https://registry.terraform.io/browse/providers]


```    
provider "aws" {
  region = "us-east-1"
}
resource "aws_instance" "vm" {
  ami           = "DUMMY_VALUE_AMI_ID"
  subnet_id     = "DUMMY_VALUE_SUBNET_ID"
  instance_type = "t3.micro"
  tags = {
    Name = "my-first-tf-node"
  }
}   
```


```
mkdir terraform_code
vim main.tf

terraform init
terraform plan
terraform apply

terraform destroy
```

