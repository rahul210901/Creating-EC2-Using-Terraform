# Create a Virtual Machine in the resource group along with virtual networks and subnets. Confirm the logins to VM after deploying the infrastructure.
# Write a custom module for multiple virtual machines deployment with the same configuration.

Firstly, we have installed Terraform and Git in our local system.
Terraform is used to write the infrastructure as a code and to write the code we use the Git's console.

Rest of the commands we have used in Gitbash :

cd documents - This command is used to change the current working directory to documents directory.

After changing the directory
we have run the command

mkdir dir1 - This command is used to make the directory in the documents directory.

cd dir1 - It will change the directory from current to dir1.

terraform init -  This command is used to initialize the Terraform in the dir1.

After running this command 

we will make files in the dir1.

 Using the vi editor and we will use .tf extension to convert the file into Terraform file.

 We have created 4 files main.tf, outputs.tf, provider.tf, terraforms.tfvars, vars.tf

 This is how we have executed our project

 ## validate, plan, apply command

terraform validate - This command is used to check whether our syntax is right or wrong.

terraform plan - This command will show a pre executed structure that what will be executed after we use the command terraform apply

terraform apply - This command will execute all the script which we have done in the files.
 






## vi main.tf

resource "aws_instance" "my-machine" {
   count = 4   # Here we are creating identical 4 machines.
   ami = var.ami
   instance_type = var.instance_type
   tags = {
      Name = "my-machine-${count.index}"
           }
}


terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 4.0"
    }
  }
}
## vi outputs.tf

output "ec2_machines" {
 # Here * indicates that there are more than one arn because count is 4
  value = aws_instance.my-machine.*.arn
}
## vi provider.tf

provider "aws" {
  region     = "ap-south-1"
  access_key = "AKIA5QUCNXXKMFZSD7NT"
  secret_key = "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"
}
## vi terraforms.tfvars

ami = "ami-0742a572c2ce45ebf"
instance_type = "t2.micro"
## vi vars.tf

# Creating a Variable for ami
variable "ami" {
  type = string
}

# Creating a Variable for instance_type
variable "instance_type" {
  type = string
}