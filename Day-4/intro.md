![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/6486f2e1-cc68-452d-8fab-94a15cfc803c)
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/5d770903-8af9-4bf9-a8f5-575d3158e22a)
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/a559a377-77a4-420b-b056-2206c54d9600)



Problems
--
1) If Github is compermized then state will be comprermized
2) Everytime someone checks out the code, update the code along we that they have to update the state file

### NOTE : The above problems can to fixed by **REMOTE BACKEND**

### Doc Ref : https://developer.hashicorp.com/terraform/language/settings/backends/s3

REMOTE BACKEND
--
- Changellens of Storing state file in external resources in AWS S3 BUCKET, You don't have worry about local terraform state file
- State file will be created in S3
- Completely restrict S3 access
- Devops engineer checks out the code and did some modification, and pushed to github, then that state will be updated in S3 bucket automatically
- Terraform init -- then it will understand that we have to use S3.
- There some so many remote backend s3 is one of them.

Explaination
--
![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/a6f7f284-2c5a-428c-b53f-e20dfead6d8c)

- wE are devopes enginerr team of 5 to 6 , we have github repo, and we have ec2 CREATION logic in the repo
- we have a github repo that hosts the terraform code and that code will have aws resouces creation logic, Ley say we are using terraform project to create EKS
- Or to crreate VPC 3 tire architecutre, what we do is instead of storing the state file in the GITHUB itself, WE WILL USE S3 BUCKET AS REMOTE BACKEND
- If any of the team member wants to change the creation logic or update, they will clone the repo, make changes and they will raise a PR back to github repo

Advantages
--
- Stores everything
- We can find differences
- On the source is based on state file

Disadvantages
--
- Stores passwords as well like policis, SNS and S3 and etc
- Any sensitive data will also we will stroes like secrets

Cooommands
--
``` terraform show ``` --Is used to show the state file

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/256007d8-53a7-470b-86e7-63358dc6a790)

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/050471d1-d0e3-42a6-8fe1-321d03efb752)

![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/33ccbc5a-0da0-4a0a-81fb-8e118d340fd5)


- GIthub repo -- with terraform code
- terraform code will have aws resouce creation logic
- like eks, vpc, s3 and etc
- we instead of storing the state fil in GIT Repo we use S3 BUCKET as remote backend
- If someone wants to use it, they will clone the repo on their laptop, apply and with the new changes they will RASIE A PR TO GITHUB REPO
- Because they execution the terraform apply command will update S3 BUCKET with the logic
- Once PR is raised someone will approve or senior member or leads once it gets merged the new code will updated (that terrform changes)
