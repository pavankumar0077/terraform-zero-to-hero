# After starting the valut service

- For demo we are using root token which will avaialbe in the console when we start the valut service

- we will get dashboard
- Secrets Engine -- If you want to use KUbernetes credentails -- then we have to configure it
- KV -- normal key value pair
- Bydefault nothing is enabled in the Hashipro valut

Hashipro valut
--
- As soon as you enter key value pair it does the encryption
- Even in the mount (the path what we give in the instance) it will store only the encrpted password
- Decrypted information is only available with hashipro valut

# Create the secrect
--
- Create secrect enginee -- give path
- add secrect -- add credentails and save it
- ![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/595b43eb-50fd-4f51-a6c1-dbfa4da93f35)

# ROLE / ACCESS to other service or applications
--
- Here we are the root user so we have access, But Terraform and Ansible doesn't have access to the valut
- WE HAVE TO CREATE A ROLE INSIDE THE HASHIPRO VALUT
- It is similar to the concept of IAM ROLE
- ![image](https://github.com/pavankumar0077/terraform-zero-to-hero/assets/40380941/a98be473-166f-4d2f-aa7e-b41701df63a4)
- eNABLE MEHTOD.
- Now we are telling hasipro valut, that i want to use app role based authentication,So i will use ANSBILE or TERRAFORM or any service
- I will authenticate TERRAFORM using this app role mechanisam

## NOTE :: YOU CAN NOT CREATE ANY ROLES USING USER INTERFACE UI 
### WE NEED TO USE CLI ITSELF.
step1 : POLICY creation (SAME AS IAM POLICY)
STEP 2 : ROLE CREATE ( SAME AS IAM ROLE)

```
vault policy write terraform - <<EOF
path "*" {
  capabilities = ["list", "read"]
}

path "secrets/data/*" {
  capabilities = ["create", "read", "update", "delete", "list"]
}

path "kv/data/*" {
  capabilities = ["create", "read", "update", "delete", "list"]
}


path "home/idrbt/*" {
  capabilities = ["create", "read", "update", "delete", "list"]
}

EOF
```
- Copy and paste in the instance where valut is running -- next new instance in same location and run the above script
- Path can be change according to the requirement

### ROLE CREATION 

```
vault write auth/approle/role/terraform \
    secret_id_ttl=10m \
    token_num_uses=10 \
    token_ttl=20m \
    token_max_ttl=30m \
    secret_id_num_uses=40 \
    token_policies=terraform

```

step 3
--
### ROLE ID AND SECRET KEY (Same like access key  and secret access key id in AWS)
```
vault read auth/approle/role/my-approle/role-id

vault read auth/approle/role/terraform/role-id
```
```
vault write -f auth/approle/role/terraform/secret-id
```

