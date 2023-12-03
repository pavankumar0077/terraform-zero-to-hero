# Terraform Wrokspace 


![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/6f95455f-e0e3-4f9b-8e78-6841f46e40a7)


- Let say there is a DEV TEAM called XYZ
- There requrirement is they want to set a EC2 instance with S3 bucket on the AWS env
- They have to do this task everything, So they created a JIRA ticket on the DEVOPS ENGINEERING TEAM Dashboard
- As a Devops we have picked this request
- So as a devops your task to create the reqest resources provides in the JIRA Ticket
- So devops carefully went to the request and find that these can can also be useful for the other teams as well commonly used task
- So that devops engineer created **MODULE** or it.
- As you wrote in the MODULAR Approach it can be resusable, Your are not solving the problem for XYZ team, but solving the problem for the future TEAMS as well.
- Along with MODULE file you also provide the README file with the instructions how to use it
- If something not getting by the README file then you will create main.tf file and write some instuctions to use it


NOTE : Now the issue this the above requirement is for the DEV team 
-
### Now we wanted create the same for Stage and prod, but they may have different resouces types like t2.large used instead of t2.medium this kind of requirements
### Let say if we have 100 env's then writing 100 times is not efficent way 

NOTE : We can do this thing, Like we write only one main.tf file 
-
- for dev env -- asking them to crete dev.tf vars file
- for stage env -- asking them to create stage.tf vars file
- for prod env -- asking them to create prod.tf vars file

### Now your thicking the problem is solved but not, We have STATEFILE (IT will record the information, let say we have executed the terraform for main.tf for dev env, So STAGEFILE will record the things 
### Now when you are executing for the STAGE env, SO NOW THE STATEFILE WILL BE OVERRIDDEN (Terraform will thing like we overridden changes for the dev env) but actually it is stage env, It wil try to delete or modify EC2 created in the dev env. Same happens with the PROD as well.

NOTE : Excepted behaviour is they need different infrastructure for Dev, Stage and PROD
-

They don't want to create for every env like one folder for dev, stage and prod.

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/1a61b31c-a0a5-435d-ab44-bd4349314538)


TO SOLVE THE ABOVE PROBELM 
-
## WE HAVE SOMETHING CALLED WORKSPACES
### WORKSPACES : Will maintain or solve the problem of single statefile [ that is causing the problem ]
### workspaces will create STATEFILE FOR THE ENV -- THAT MEANS 
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/274744b6-bb22-42c6-ba4d-98285e1e7063)

-- Their will a folder created terraform state.d 
-- Inside this there will a folder for DEV,STAGE AND PROD (Depending up on how many env's do you create) or how many workspaces do you ccreate if you create 100 workspaces with in the same folder within the same project you will have folders for each env inside the each folder we have state file.
-- Now when you are in Dev worksapce dev statefile will be executed, when we are in stage then stage statefile will be executed. same with prod as well
-- Now the STATEFILE are not overlapping

Commands
--
``` terraform apply -var-file=stage.tfvars ``` To apply another terraform config.

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/b38a78e3-2f21-44e0-abe4-6ec7e90d192f)

- Here existing infra is modifing, but not creating for each env
- To solve this issue we have to use **TERRAFORM WORKSPACE**

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/694138b2-9bd7-4b60-80e8-7d7eda4b2c88)

Commands
--
To create workspace
--
```
terraform workspace new dev
```
- To create dev env

```
terrform workspace new stage
```
- To create stage env and same for prod as well

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/097387d4-cf02-4dc8-9571-dbe0e8ed2299)

```
terraform workspace -h
```
- Used to check all the available tags for the commans

```
terraform workspace select dev
```
- Used to switch between workspaces

```
terraform workspace show
```
- Used to check in which workspace you are in

### Now i swtiched to dev workspace and used init and apply commands
- SO STATEFILE is created only in the dev env

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/6c22705c-c951-4ea4-aacd-6b1db0b19187)

### Now i switched to stage worksapce and used apply commands used t2.medium
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/e57e32ef-3e22-461f-9067-e275c3efa254)
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/b862d496-a625-4b87-8da4-a949cd324cae)

- micro is dev env instance
- medium is stage env instance

## Now delete the resouces 
- switch the dev
- terraform destroy
- same for other env's as well

Ways to work with tfvars file for different env's
==

1ST WAY
--
### Now we are update the terraform.tf vars file every time to change the insttace type 
```
terraform apply -var-file=prod.tfvars
```
- Like this.
- For this we need to create tfvars file for each and every env and apply accordingly 

2ND WAY
--
- Go to main.tf file
- Before changes
- ![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/1b8854ea-c1b4-46b8-a992-19e90b7cf2c6)
- ![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/4d2e21aa-a21c-40b7-9000-50a754afe0f6)
- After changes
- NOW REMOVE THE VALUES FORM TERRAFORM.TFVARS FILE
```
provider "aws" {
  region = "us-east-1"
}

variable "ami" {
    description = "value"
  
}

# variable "instance_type" {
#   description = "value"
# }

variable "instance_type" {
  description = "value"
  type = map(string)

  default = {
    "dev" = "t2.micro"
    "stage" = "t2.medium"
    "prod" = "t2.xlarge"
  }
}


module "ec2_instance" {
    source = "./modules/ec2_instance"
    ami = var.ami
    instance_type = lookup(var.instance_type, terraform.workspace, "t2.micro")
  
}
```
- Here in the ``` instance_type = lookup(instance_type, terraform.workspace, "t2.micro") ```
- Lookup will look for the map, (instance type, workspace - like in which workspace it is, and here t2.micor is the default if there is not workspace available with the name mentioned then t2.micro will will applied)
### Now when i try to apply in prod or stage env we can do it without changing the terraform.tfvars file everytime.
