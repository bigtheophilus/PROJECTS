# AUTOMATING AWS INFRASTRUCTURES IN CODE USING TERRAFORM

## OBJECTIVE: in this project i just provisioned two major aws_resources  (aws_vpc and subnets) using terraform. what terraform does is to automate the provisioning of this resources within 10secs provided the block of codes are validated. the effication of refactoring avoiding hard coding is ensured using variables and values with the creation of variable.tf and terraform.ftvars. variable.tf contained all the decleared variables while the terraform.ftvars contain all the values.

### Another feature in this project was the configuration of my awscli so that my local working enviroment(work station) can communicate with my aws account. this was achiched by creating an IAM account,a group and a user called `terraform` while granting administrator access to the group which also give such privileges to the user `terraform`. through the creation of a secrete_key and access_key, aws_configure was established. S3 bucket was created though not majorly used but to test that we can communicate to our aws infrastructure after the aws configuration usinf the python boto3 feature. it is important to note that this project was completed on windows hence gitbash was used.

## STEP1: user `terraform` created and aws_configure on workstation
![alt text](images/user_terraform_created-1.png)

### creating serete_key and access_key
![alt text](images/terraform_user_keys_created-2.png)
![alt text](images/terraform_user_summary_details-3.png)

### `aws configure`
![alt text](images/aws_config_for_user_acces-4.png)

### S3_bucket created (divine-dev-terraform-bucket) and using the boto3 feature 
![alt text](images/bucket_created-5.png)
![alt text](images/python_file_wt_boto3_codes.png)

## STEP2: creation of a folder called PBL and inside created a file called main.tf
![alt text](images/cd_PBL_to_terraforn_init-10.png)

### block of codes for vpc_provisioning:
![alt text](images/main_tf_vpc_provisioning_codes.png)
![alt text](images/terraform_plan_output-13.png)

### confirmed vpc_provisioned on console
![alt text](images/confirmed_vpc_created_on_console.png)


#### had some error and resolved by commentig out the paths
![alt text](images/error_on_terraform_plan-commented_out_path.png)
![alt text](images/error_terraform_plan_commented_out-12.png)


### note that before running the `terraform apply` and `terraform plan` i ran `terraform init` which help to download all the aws dependencies and infracture file so that hashicorn can have the aws depencies in its registry.
![alt text](images/cd_PBL_to_terraforn_init-10.png)

# NOTE: the function of the `terraform.tfstate` file that is created upon `terraform apply` is to keep updated of the current `state of the infrastructure` created while the `terraform.tfstate.lock.info`(created upon terraform init) is used to keep track on the user running the code at a point in time . this is to prevent duplication of infrastructuer incase of two users trying to provision the same infrastructure concurrently.
![alt text](images/terraform_lock_file_wt_provider_info.png)

## STEP3: `creating subnetd using code Refactoring`.
## Going forward using refacturing to avoid hard coding and complicate my block of codes, created variable.tf and terraform.tfvars to declear the variables and declear the values respectively.
![alt text](images/variables.tf_created_to_declear_variables.png)
![alt text](images/approved_variable.tf_file.png)
![alt text](images/terraform.tfvars_created_to_declear_values_variables.png)
![alt text](images/approved_terraform.tfvars_file.png)


### `terraform plan`
![alt text](images/terraform_plan_output1-general.png)
![alt text](images/terraform_plan_output2-general.png)

## `terraform apply`: look at the outlook of final block of code in the main.tf file
![alt text](images/approved_main.tf_file.png)
![alt text](images/confirmed_subnets_on_console.png)



## Note that the major bottelneck in this project was how to use the boto3 feature. through a mentor i got to know that a file `main.py` and run the code in it 
![alt text](images/error_on_boto3_instalation.png)
![alt text](images/installed_boto3-6.png)

### resolved

![alt text](images/python_file_wt_boto3_codes.png)

# CONGRANTULATION!!!!!!!!!






