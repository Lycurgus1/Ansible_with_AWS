
![logo](images/ansible_logo.png)     ![logo](images/aws_logo.png)

# Ansible and AWS

- This directory is about setting up Ansible with AWS
- It contains set up instructions to enable the creation of an AWS instance with Ansible

## Dependencies

- Git bash
- Virtual box manager and vagrant is recommend
	- This will enable you to set this up in a virtual machine
	- Else you could set this up in your operating system

- It is recomended to follow the steps in the Ansible directory before moving onto this directory
	- It contains theory and basic ansible set up steps

- Note: Most of these steps were gained from the linked below

```https://medium.com/datadriveninvestor/devops-using-ansible-to-provision-aws-ec2-instances-3d70a1cb155f```

## Steps

### 1. Create an AWS user

- Then follow these steps and take note of your access and secret key

```https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console```

### 2. Install Ansible and the EC2 module dependencies

```
sudo apt install python
sudo apt install python-pip
pip install boto boto3 ansible
```

### 3. Create SSH keys to connect to the EC2 instance after provisioning

```ssh-keygen -t rsa -b 4096 -f ~/.ssh/my_aws```

### 4. Create the Ansible directory structure

```
sudo mkdir -p AWS_Ansible/group_vars/all/
cd AWS_Ansible
sudo touch playbook.yml
```

### 5. Create Ansible Vault file to store the AWS Access and Secret keys

```ansible-vault create group_vars/all/pass.yml```

- You will need to enter a password
- Once done exit the vault with ctrl c, then on screen instructions

### 6. Edit the pass.yml file and create the keys global constants

```ansible-vault edit group_vars/all/pass.yml```

- Enter your access and secret key (got from setting up as user) into the file as per the below format
	- If in engineering 67 this has been given to you

```
ec2_access_key: AAAAAAAAAAAAAABBBBBBBBBBBB                                      
ec2_secret_key: afjdfadgf$fgajk5ragesfjgjsfdbtirhf
```

- To exit press esc, then type enter :wq + <Enter> to save and exit

### 7. Edit the playbook.yml file per the playbook file in this directory

- You will need to change the permissions of this file

```sudo chmod 666 pass.yml```

### 8. Run ansible to set up the instance

```ansible-playbook playbook.yml --ask-vault-pass --tags create_ec2```

### 9. Connect to the instance

```ssh -i ~/.ssh/my_aws ubuntu@ec2-18-218-148-27.us-east-2.compute.amazonaws.com```

- The region and ec2 IP will change in the command


## Common Errors

- You may not have permission to run commands if running in /etc/ansible
	- If there either use sudo or go into root mode with sudo su
