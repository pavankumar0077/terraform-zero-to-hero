Requirement
--
Step 1:
--
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/f07a7991-ff91-4cf5-a0ff-f8529cd8b87c)

- Dev team xyz -- Has a requirement -- when modified that application -- flask app
- Whenever they modify the applicaiton code -- they want the Devops teams -- to create the terraform project
- To Test their changes they want us to create a VPC
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

