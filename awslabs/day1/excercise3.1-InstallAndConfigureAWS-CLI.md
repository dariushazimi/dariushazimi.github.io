# Day 1
# Excercise 2.1

## Shared Responsibility Model
![Getting Started](
https://d1.awsstatic.com/security-center/Shared_Responsibility_Model_V2.59d1eccec334b366627e9295b304202faf7b899b.jpg)

### Best Practices for Securing your aws account

AWS recommends several best practices for securing your AWS account: 
1. Require MFA for root-level access.
2. Do not share root credentials with anyone other than the account holder.
3. Physically secure root account hardware MFA devices in a safe place, such as a vault.
4. Create individual IAM users. 
5. ​Use groups to assign permissions to IAM users. 
6. Enable MFA for privileged users. 
7. Use IAM roles for applications that run on Amazon EC2 instances.
8. Delegate by using IAM roles instead of sharing credentials. 
9. Rotate credentials regularly. 
10. Remove unnecessary credentials. 
11. Use policy conditions for extra security. 
12. Monitor activity on your AWS account. Remove root credentials.
13. Use access levels to review IAM permissions. 
14. Use AWS-defined policies to assign permissions whenever possible.
15. Use IAM roles to provide cross-account access. 

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

## Set your profile
```
Linux, OS X Example:

$ export AWS_DEFAULT_PROFILE=account1
$ aws dynamodb list-tables
Windows Example:

$ set AWS_DEFAULT_PROFILE=account1
$ aws s3 ls
```

## Create user account

`aws iam create-user --user-name user1`

1. Assign password
2. Add user to a group, if you don't have a group created yet, create one called EC2-Admin group
3. Login as the newly created user

## Excercise 3.1

### Creating AWS Identity and Access Management (IAM) Users 
Create three IAM user accounts with the user names Alice, Bob, and Charlie with the AWS CLI using the aws iam create-user command example:
 `aws iam create-user --user-name Alice` 
 
 Take note of the information returned: 

```
{
    "User": {
        "UserName": "Alice",
        "Path": "/",
        "CreateDate": "2017-04-25T00:54:38.139Z",
        "UserId": "AIDAI3QWSE7XYB6ERAQVC",
        "Arn": "arn:aws:iam::123456789012:user/Alice"
    }
}
```
## Excercise 3.2
### Create IAM Credentials. 
Now you will create credentials for the three IAM users that you created. You will use the aws iam create-login-profile and the aws iam create-access-key commands to complete this exercise. Alice will need to access the AWS Management Console and the AWS CLI. Therefore she will need to have a password and access key generated. 
See the following examples for the CLI commands and related outputs.
1. Create a password for Alice. 
2. Generate access keys for Alice. `aws iam create-login-profile --user-name Alice --password yamaha@stryker1`
```
{
    "LoginProfile": {
        "UserName": "Alice",
        "CreateDate": "2017-04-25T01:01:53.417Z",
        "PasswordResetRequired": false
    }
}
aws iam create-access-key --user-name Alice
{
    "AccessKey": {
        "UserName": "Alice",
        "Status": "Active",
        "CreateDate": "2017-04-25T01:06:07.127Z",
        "SecretAccessKey": "blDyMBCKLFGCgiZUM9q3exXnbljOhhlrBSRx32WF",
        "AccessKeyId": "AKIAIMGMTCVJV53AGT5A"
    }
}
```
3. Create a password for Bob. He will only have access to the AWS Management Console—no access keys are required. 
4. Charlie will be your Amazon EC2 and Amazon S3 administrator. He needs access to the AWS CLI, but does not need access to the AWS Management Console.
## Excercise 3.3
### Create IAM Groups
In this exercise, you will create IAM groups and add your IAM users to the groups. You will use the aws iam create-group and aws iam add-user-to-group commands to complete this exercise. Create the following:

| Groups    | Users   |
|-----------|---------|
| admins    | Alice   |
| Monitors  | Bob     |
| Operators | Charlie |

`aws iam create-group --group-name admins`
```
{
    "Group": {
        "Path": "/",
        "CreateDate": "2017-04-25T01:22:20.505Z",
        "GroupId": "AGPAIKTFN6QVR4M226BYA",
        "Arn": "arn:aws:iam::123456789012:group/admins",
        "GroupName": "admins"
    }
}
```

`aws iam add-user-to-group --group-name admins --user-name Alice`

## Excercise 3.4 Working with IAM Policies 

This exercise focuses on using AWS Managed Policies as the basis of the permissions that you set for the IAM groups. In this exercise, you will use the AWS Management Console. 
1. Log in to the console with a user who has IAM permissions. For this exercise, the root account will work just fine, as you are creating your IAM accounts. After you have created an IAM account with admin access (for example, Alice) you can put the root account to rest. 
2. Go to the IAM console. 
3. Navigate to Groups. 
4. Select the Admin group. 
5. Go to the permissions tab, and attach the AdministratorAccess policy. 
6. Click on Show Policy to verify that you have administrator access.
7. Perform the same steps for the monitors group, and assign ReadOnlyAccess. 
8. Perform the same steps for the operators group, and assign the AmazonEC2FullAccess policy.
## Excercise 3.5
### Working with IAM Roles
 So far you have created IAM user accounts, IAM groups, and attached IAM policies to those groups. Now you will create a role that will allow an Amazon EC2 instance acting as a bastion host in order to interact with the EC2 and Amazon S3 services. The bastion host will be able to create, modify, or terminate any EC2 instance and interact with S3 resources—all without having to store credentials on the bastion host. 
 1. Log in to the AWS Management Console. 
 2. Go to the IAM console. 
 3. ​Click on Dashboard. 
 4. Take note of the IAM Users Sign-In link. 
 5. Click on the link, and sign in as Alice. 
 6. Go back to the IAM console. 
 7. Navigate to Roles, and select the Amazon EC2 AWS Service Role. 
 8. Create a new role, and attach the AmazonEC2FullAccess and AmazonS3FullAccess policy to this role. 
 9. Name your IAM Role bastionHost. (Your role will be tested in the next exercises.)