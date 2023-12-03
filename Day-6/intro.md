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
