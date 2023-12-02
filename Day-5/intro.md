Requirement
--
Step 1:
--
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/f07a7991-ff91-4cf5-a0ff-f8529cd8b87c)

- Dev team xyz -- Has a requirement -- when modified that application -- flask app
- Whenever they modify the applicaiton code -- they want the Devops teams -- to create the terraform project
- To Test their changes they want us to
- create a VPC
- 1. Public Subnet -- (We need to create subnet first ) for that we need to create Route table and destination of the route table is Internet Gateway
  2. Route Table
  3. Internet Gateway
  4. We need to associate Route table to the subnet so that we will become Public subnet as it is connected to IGW
  5. Create EC2 -- and application file to the external link. -- And configure the security group accordingly.
  6. Dev team wants to verify that their applicaiton is working fine or not.

note: user-date in EC2 is only for small projects not situable for complex projects.

Step 2:
--
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/c355e44c-8159-41f5-b6c7-25ada402988a)

Integrating with CICD
--
- Github --> Webhook --> Jenkins --> Terraform resource creation

Provisioners
--
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/84a679f3-fcf1-476f-bfd8-19b87b2330a7)

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/bbaeb9b7-5c86-4593-bbf1-0280b9d4ca9d)

-- Remote exec provisioner -- At the time of creating EC2 instance itself, You can connec to that particular instance and execute the commands like python, java or any commands
-- Local exec -- Ex: We want to print something on the screen, Like echo steps like 1,2... etc, If we have 10,000 lines to print, then we are asking terraform to save this in a file.
-- File provisioner -- Used to copy the files, Let say we have ec2 and we want to copy 10 files, using file provisioner we can do it.

- Provisioners -- To execute + implement some actions during the creations
- At the time of creation of ec2 instances we have copied and executed some commands
- Provisioner is the concept in terraform that will let you to copy and execute particualr actions
- We can also use provisioner at the time of destrction (deletion)

-- As a devops engineers we have some challenges with terraform example - if we don't have provisioner then we have to use ansible or shell scripts 

To solve the above chanllenge terraform provides
--
- One is Remote exec provisioner -- At the time creating EC2 instances itself we can connnect to the particular instance itself we can execute any command like install python, java and etc any shell commands
- Secons is Local exec provisioner -- During the creation itself we can provide like create echo statements like terraform done 2/8 tasks like that, or create file a and all the resouces in the console can be saved in file
- File provisioner -- Used to copy the files, Let say we have ec2 and we want to copy 10 files, using file provisioner we can do it.



