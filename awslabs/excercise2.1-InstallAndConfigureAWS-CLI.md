# Day 1
# Excercise 2.1
## Install and Configure AWS CLI on Windows With MSI
1. Begin by logging in to the AWS Management Console with your user name, password, and MFA device (if applicable). 
2. Navigate to the IAM service. 
3. Select Security, and then click on your user name. 
4. Under Security Credentials, click Create Access Key. 
5. Before closing the dialog box that appears, save your access key and secret key in a safe place. 
6. Download the MSI Installer (https://s3.amazonaws.com/aws-cli/AWSCLI64.msi). ​
7. Run the downloaded MSI installer. 
8. Follow the instructions that appear. 
9. Open a command prompt. 
10. Type `aws –version` 
11. Configure the AWS CLI by running the command `aws configure` and filling in the access key and secret key that you obtained in Step 5. Optionally (but highly recommended), specify a default region, such as us-east-2. Also optionally, specify a default format type.
12. Test that you have set up the AWS CLI correctly and can connect to the AWS API endpoints by running the command `aws ec2 describe-availability-zones`. The AWS CLI should return a list of the available Availability Zones in your default region.

## On Linux or Mac
If Python isn’t installed on your system, install it using the directions at http://www.python.org/. If pip isn’t installed on your system, install it using the directions at https://pip.pypa.io/en/stable/installing/. Install the AWS CLI using the command `pip install awscli --upgrade --user`.

# Set your profile
```
Linux, OS X Example:

$ export AWS_DEFAULT_PROFILE=account1
$ aws dynamodb list-tables
Windows Example:

$ set AWS_DEFAULT_PROFILE=account1
$ aws s3 ls
```

# Create user account
`aws iam create-user --user-name user1`

1. Assign password
2. Add user to a group, if you don't have a group created yet, create one called EC2-Admin group
3. Login as the newly created user
