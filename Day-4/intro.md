![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/6486f2e1-cc68-452d-8fab-94a15cfc803c)

Advantages
--
- Stores everything
- We can find differences
- On the source is based on state file

Disadvantages
--
- Stores passwords as well like policis, SNS and S3 and etc
- Any sensitive data will also we will stroes like secrets

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
