# AWS Security Guidelines Foundation Framemework
This document provides prescriptive guidance for configuring security options
for a subset of Amazon Web Services with an emphasis on foundational, testable,
and architecture agnostic settings. Specific Amazon Web Services in scope for
this document include:

-   AWS Identity and Access Management (IAM)
-   AWS Config
-   AWS CloudTrail
-   AWS CloudWatch
-   AWS Simple Notification Service (SNS)
-   AWS Simple Storage Service (S3)
-   AWS VPC (Default)

Intended Audience 
------------------

This document is intended for system and application administrators, security
specialists, auditors, help desk, platform deployment, and/or DevOps personnel
who plan to develop, deploy, assess, or secure solutions in Amazon Web Services.

Consensus Guidance 
-------------------

This benchmark was created using a consensus review process comprised of subject
matter experts. Consensus participants provide perspective from a diverse set of
backgrounds including consulting, software development, audit and compliance,
security research, operations, government, and legal.

Based on this benchmark AWS has also created security hub service which
essentially covers all the recommendations covered in this document.

Some of the code snippets have been modified since some of the code provided
produced errors during testing and validation. These code snippets have been
highlighted to show the correct format.

Typographical Conventions 
--------------------------

The following typographical conventions are used throughout this guide:

| Convention              | Meaning                                                                                       |                                                                                                         |
|-------------------------|-----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
|                         | Stylized Monospace font                                                                       | Used for blocks of code, command, and script examples. Text should be interpreted exactly as presented. |
|                         |                                                                                               |                                                                                                         |
| Monospace font          | Used for inline code, commands, or examples. Text should be interpreted exactly as presented. |                                                                                                         |
| *\<font in brackets\>*  | Texts set in angle brackets denote a variable requiring substitution for a real value.        |                                                                                                         |
| *Italic font*           | Used to denote the title of a book, article, or other publication.                            |                                                                                                         |
| **Note**                | Additional information or caveats                                                             |                                                                                                         |
| Modified Snippets       | The original code produced errors. The modified version worked and was tested.                |                                                                                                         |

Scoring Information 
--------------------

A scoring status indicates whether compliance with the given recommendation
impacts the assessed target's benchmark score. The following scoring statuses
are used in this benchmark:

**Scored**

Failure to comply with "Scored" recommendations will decrease the final
benchmark score. Compliance with "Scored" recommendations will increase the
final benchmark score.

**Not Scored**

Failure to comply with "Not Scored" recommendations will not decrease the final
benchmark score. Compliance with "Not Scored" recommendations will not increase
the final benchmark score.

No scoring have been used in this document but the indicators (scored, Not
scored) have been kept for reference.

Profile Definitions 
--------------------

The following configuration profiles are defined by this Benchmark:

-   **Level 1**

>   Items in this profile intend to:

-   be practical and prudent;

-   provide a clear security benefit; and

-   not inhibit the utility of the technology beyond acceptable means.

-   **Level 2**

>   This profile extends the "Level 1" profile. Items in this profile exhibit
>   one or more of the following characteristics:

-   are intended for environments or use cases where security is paramount

-   acts as defense in depth measure

-   may negatively inhibit the utility or performance of the technology.

Recommendations
================

Summary Table 
====================================

| **Control**  | **Set Correctly**                                                                                                |    |     |     |
|--------------|------------------------------------------------------------------------------------------------------------------|----|-----|-----|
|              |                                                                                                              | No | Yes |    N/A |
| **1**        | **Identity and Access Management**                                                                               |    |     |     |
| 1.1          | Avoid the use of the "root" account (Scored)                                                                     |   |    |     |
| 1.2          | Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a console password (Scored)      |   |    |  |
| 1.3          | Ensure credentials unused for 90 days or greater are disabled (Scored)                                           |   |    |     |
| 1.4          | Ensure access keys are rotated every 90 days or less (Scored)                                                    |   |    |     |
| 1.5          | Ensure IAM password policy requires at least one uppercase letter (Scored)                                       |   |    |     |
| 1.6          | Ensure IAM password policy require at least one lowercase letter (Scored)                                        |   |    |     |
| 1.7          | Ensure IAM password policy require at least one symbol (Scored)                                                  |   |    |  |
| 1.8          | Ensure IAM password policy require at least one number (Scored)                                                  |   |    |     |
| 1.9          | Ensure IAM password policy requires minimum length of 14 or greater (Scored)                                     |   |    |  |
| 1.10         | Ensure IAM password policy prevents password reuse (Scored)                                                      |   |    |  |
| 1.11         | Ensure IAM password policy expires passwords within 90 days or less (Scored)                                     |   |    |     |
| 1.12         | Ensure no root account access key exists (Scored)                                                                |   |    |     |
| 1.13         | Ensure MFA is enabled for the "root" account (Scored)                                                            |   |    |  |
| 1.14         | Ensure hardware MFA is enabled for the "root" account (Scored)                                                   |   |    |  |
| 1.15         | Ensure security questions are registered in the AWS account (Not Scored)                                         |   |    |  |
| 1.16         | Ensure IAM policies are attached only to groups or roles (Scored)                                                |   |    |     |
| 1.17         | Maintain current contact details (Not Scored)                                                                    |   |    |     |
| 1.18         | Ensure security contact information is registered (Not Scored)                                                   |   |    |     |
| 1.19         | Ensure IAM instance roles are used for AWS resource access from instances (Not Scored)                           |   |    |     |
| 1.20         | Ensure a support role has been created to manage incidents with AWS Support (Scored)                             |   |    |     |
| 1.21         | Do not setup access keys during initial user setup for all IAM users that have a console password (Not Scored)   |   |    |     |
| 1.22         | Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored)                   |   |    |     |
| **2**        | **Logging**                                                                                                      |    |     |     |
| 2.1          | Ensure CloudTrail is enabled in all regions (Scored)                                                             |   |    |     |
| 2.2          | Ensure CloudTrail log file validation is enabled (Scored)                                                        |   |    |     |
| 2.3          | Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored)                           |   |    |     |
| 2.4          | Ensure CloudTrail trails are integrated with CloudWatch Logs (Scored)                                            |   |    |     |
| 2.5          | Ensure AWS Config is enabled in all regions (Scored)                                                             |   |    |     |
| 2.6          | Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket (Scored)                                  |   |    |     |
| 2.7          | Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored)                                             |   |    |    |
| 2.8          | Ensure rotation for customer created CMKs is enabled (Scored)                                                    |   |    |    |
| 2.9          | Ensure VPC flow logging is enabled in all VPCs (Scored)                                                          |   |    |     |
| **3**        | **Monitoring**                                                                                                   |    |     |     |
| 3.1          | Ensure a log metric filter and alarm exist for unauthorized API calls (Scored)                                   |   |    |     |
| 3.2          | Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored)                   |   |    |     |
| 3.3          | Ensure a log metric filter and alarm exist for usage of "root" account (Scored)                                  |   |    |     |
| 3.4          | Ensure a log metric filter and alarm exist for IAM policy changes (Scored)                                       |   |    |     |
| 3.5          | Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored)                         |   |    |     |
| 3.6          | Ensure a log metric filter and alarm exist for AWS Management Console authentication failures (Scored)           |   |    |     |
| 3.7          | Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs (Scored) |   |    |    |
| 3.8          | Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored)                                 |   |    |     |
| 3.9          | Ensure a log metric filter and alarm exist for AWS Config configuration changes (Scored)                         |   |    |     |
| 3.10         | Ensure a log metric filter and alarm exist for security group changes (Scored)                                   |   |    |     |
| 3.11         | Ensure a log metric filter and alarm exist for changes to Network Access Control Lists (NACL) (Scored)           |   |    |     |
| 3.12         | Ensure a log metric filter and alarm exist for changes to network gateways (Scored)                              |   |    |     |
| 3.13         | Ensure a log metric filter and alarm exist for route table changes (Scored)                                      |   |    |     |
| 3.14         | Ensure a log metric filter and alarm exist for VPC changes (Scored)                                              |   |    |     |
| **4**        | **Networking**                                                                                                   |    |     |     |
| 4.1          | Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 (Scored)                                       |   |    |     |
| 4.2          | Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 (Scored)                                     |   |    |     |
| 4.3          | Ensure the default security group of every VPC restricts all traffic (Scored)                                    |   |    |  |
| 4.4          | Ensure routing tables for VPC peering are "least access" (Not Scored)                                            |   |    |    |

Recommendations 
================

*1 Identity and Access Management* 
-----------------------------------

This section contains recommendations for configuring identity and access
management related options.

#### 1.1 Avoid the use of the "root" account (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

The "root" account has unrestricted access to all resources in the AWS account.
It is highly recommended that the use of this account be avoided.

**Rationale:**

The "root" account is the most privileged AWS account. Minimizing the use of
this account and adopting the principle of least privilege for access management
will reduce the risk of accidental changes and unintended disclosure of highly
privileged credentials.

**Audit:**

Implement the Ensure a log metric filter and alarm exist for usage of "root"
account recommendation in the Monitoring section of this benchmark to receive
notifications of root account usage. Additionally, executing the following
commands will provide ad-hoc means for determining the last time the root
account was used:

aws iam generate-credential-report

aws iam get-credential-report --query 'Content' --output text \| base64 -d \|
cut -d, -f1,5,11,16 \| grep -B1 '\<root_account\>'

Note: there are a few conditions under which the use of the root account is
required, such as requesting a penetration test or creating a CloudFront private
key.

**Remediation:**

Follow the remediation instructions of the Ensure IAM policies are attached only
to groups or roles recommendation

**References:**

1.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

**CIS Controls:**

4.3 *Ensure the Use of Dedicated Administrative Accounts*

Ensure that all users with administrative account access use a dedicated or
secondary account for elevated activities. This account should only be used for
administrative activities and not internet browsing, email, or similar
activities.

#### 1.2 Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a console password (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Multi-Factor Authentication (MFA) adds an extra layer of protection on top of a
user name and password. With MFA enabled, when a user signs in to an AWS
website, they will be prompted for their user name and password as well as for
an authentication code from their AWS MFA device. It is recommended that MFA be
enabled for all accounts that have a console password.

**Rationale:**

Enabling MFA provides increased security for console access as it requires the
authenticating principal to possess a device that emits a time-sensitive key and
have knowledge of a credential.

**Audit:**

Perform the following to determine if a MFA device is enabled for all IAM users
having a console password:

Via Management Console

1.  Open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the left pane, select Users

3.  If the MFA Device or Password columns are not visible in the table, click
    the gear icon at the upper right corner of the table and ensure a checkmark
    is next to both, then click Close .

4.  Ensure each user having a checkmark in the Password column also has a value
    in the MFA Device column.

Via the CLI

1.  Run the following command (OSX/Linux/UNIX) to generate a list of all IAM
    users along with their password and MFA status:

aws iam generate-credential-report

aws iam get-credential-report --query 'Content' --output text \| base64 -d \|
cut -d, -f1,4,8

1.  The output of this command will produce a table similar to the following:

user,password_enabled,mfa_active elise,false,false brandon,true,true
rakesh,false,false helene,false,false paras,true,true anitha,false,false

1.  For any column having password_enabled set to true , ensure mfa_active is
    also set to true.

**Remediation:**

Perform the following to enable MFA:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the navigation pane, choose Users.

3.  In the User Name list, choose the name of the intended MFA user.

4.  Choose the Security Credentials tab, and then choose Manage MFA Device.

5.  In the Manage MFA Device wizard, choose A virtual MFA device, and then
    choose Next Step.

IAM generates and displays configuration information for the virtual MFA device,
including a QR code graphic. The graphic is a representation of the 'secret
configuration key' that is available for manual entry on devices that do not
support QR codes.

1.  Open your virtual MFA application. (For a list of apps that you can use for
    hosting virtual MFA devices, see [Virtual MFA
    Applications.](http://aws.amazon.com/iam/details/mfa/#Virtual_MFA_Applications))
    If the virtual MFA application supports multiple accounts (multiple virtual
    MFA devices), choose the option to create a new account (a new virtual MFA
    device).

2.  Determine whether the MFA app supports QR codes, and then do one of the
    following:

-   Use the app to scan the QR code. For example, you might choose the camera
    icon or choose an option similar to Scan code, and then use the device's
    camera to scan the code.

-   In the Manage MFA Device wizard, choose Show secret key for manual
    configuration, and then type the secret configuration key into your MFA
    application.

When you are finished, the virtual MFA device starts generating one-time
passwords.

8. In the Manage MFA Device wizard, in the Authentication Code 1 box, type the
one-time password that currently appears in the virtual MFA device. Wait up to
30 seconds for the device to generate a new one-time password. Then type the
second one-time password into the Authentication Code 2 box. Choose Active
Virtual MFA.

**Forced IAM User Self-Service Remediation**

Amazon has published a pattern that forces users to self-service setup MFA
before they have access to their complete permissions set. Until they complete
this step, they cannot access their full permissions. This pattern can be used
on new AWS accounts. It can also be used on existing accounts - it is
recommended users are given instructions and a grace period to accomplish MFA
enrollment before active enforcement on existing AWS accounts. [How to Delegate
Management of Multi-Factor Authentication to AWS IAM Users
](http://blogs.aws.amazon.com/security/post/Tx2SJJYE082KBUK/How-to-Delegate-Management-of-Multi-Factor-Authentication-to-AWS-IAM-Users)

**References:**

1.  [http://tools.ietf.org/html/rfc6238 ](http://tools.ietf.org/html/rfc6238)

2.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html)

**CIS Controls:**

4.5 *Use Multifactor Authentication For All Administrative Access*

Use multi-factor authentication and encrypted channels for all administrative
account access.

#### 1.3 Ensure credentials unused for 90 days or greater are disabled (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

AWS IAM users can access AWS resources using different types of credentials,
such as passwords or access keys. It is recommended that all credentials that
have been unused in 90 or greater days be removed or deactivated.

**Rationale:**

Disabling or removing unnecessary credentials will reduce the window of
opportunity for credentials associated with a compromised or abandoned account
to be used.

**Audit:**

Perform the following to determine if unused credentials exist:

**Download Credential Report:** Using Management Console:

1.  Login to the AWS Management Console

2.  Click Services

3.  Click IAM

4.  Click on Credential Report

5.  This will download an .xls file which contains credential usage for all
    users within an AWS Account - open this file

Via CLI

1.  Run the following commands:

| aws iam generate-credential-report aws iam get-credential-report --query 'Content' --output text \| base64 -d \| cut -d, -f1,4,5,6,9,10,11,14,15,16 |
|-----------------------------------------------------------------------------------------------------------------------------------------------------|


**Ensure unused credentials does not exist:**

1.  For each user having password_enabled set to TRUE , ensure
    password_last_used_date is less than 90 days ago.

2. When password_enabled is set to TRUE and password_last_used is set to
No_Information , ensure password_last_changed is less than 90 days ago.

1. For each user having an access_key_1_active or access_key_2_active to
TRUE , ensure the corresponding access_key_n_last_used_date is less than 90
days ago.

When a user having an access_key_x_active (where x is 1 or 2) to TRUE and
corresponding access_key_x_last_used_date is set to N/A',
ensureaccess_key_x_last_rotated\` is less than 90 days ago.

**Remediation:**

Perform the following to remove or deactivate credentials:

1.  Login to the AWS Management Console:

2.  Click Services

3.  Click IAM

4.  Click on Users

5.  Click on Security Credentials

6.  As an Administrator Click on Make Inactive for credentials that have not been used in 90 Days

7. As an IAM User
Click on Make Inactive or Delete for credentials which have not been used
in 90 Days



16.9 *Disable Dormant Accounts*

Automatically disable dormant accounts after a set period of inactivity.

#### 1.4 Ensure access keys are rotated every 90 days or less (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Access keys consist of an access key ID and secret access key, which are used to
sign programmatic requests that you make to AWS. AWS users need their own access
keys to make programmatic calls to AWS from the AWS Command Line Interface (AWS
CLI), Tools for Windows PowerShell, the AWS SDKs, or direct HTTP calls using the
APIs for individual AWS services. It is recommended that all access keys be
regularly rotated.

**Rationale:**

Rotating access keys will reduce the window of opportunity for an access key
that is associated with a compromised or terminated account to be used.

Access keys should be rotated to ensure that data cannot be accessed with an old
key which might have been lost, cracked, or stolen.

**Audit:**

Perform the following to determine if access keys are rotated as prescribed:

1.  Login to the AWS Management Console

2.  Click Services

3.  Click IAM

4.  Click on Credential Report

5.  This will download an .xls file which contains Access Key usage for all IAM
    users within an AWS Account - open this file

6.  Focus on the following columns (where x = 1 or 2)

-   access_key_X_active

-   access_key_X_last_rotated

>   7. Ensure all active keys have been rotated within 90 days

Via CLI

`aws iam generate-credential-report`

`aws iam get-credential-report --query 'Content' --output text \| base64 -d`

**Remediation:**

Perform the following to rotate access keys:

1.  Login to the AWS Management Console:

2.  Click Services

3.  Click IAM

4.  Click on Users

5.  Click on Security Credentials

6.  As an Administrator Click on Make Inactive for keys that have not been rotated in 90 Days

7. As an IAM User

Click on Make Inactive or Delete for keys which have not been rotated or used in 90 Days

1.  Click on `\` Create Access Key

2.  Update programmatic call with new Access Key credentials

Via CLI

aws iam update-access-key aws iam create-access-key aws iam delete-access-key


16 *Account Monitoring and Control*

Account Monitoring and Control

#### 1.5 Ensure IAM password policy requires at least one uppercase letter (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Password policies are, in part, used to enforce password complexity
requirements. IAM password policies can be used to ensure password are comprised
of different character sets. It is recommended that the password policy require
at least one uppercase letter.

**Rationale:**

Setting a password complexity policy increases account resiliency against brute
force login attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Requires at least one uppercase letter" is checked under "Password
    Policy"

Via CLI

aws iam get-account-password-policy

Ensure the output of the above command includes "RequireUppercaseCharacters":
true

**Remediation:**

Perform the following to set the password policy as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Requires at least one uppercase letter"

>   Click "Apply password policy"

Via CLI

`aws iam update-account-password- --require-uppercase-characters`

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.

#### 1.6 Ensure IAM password policy require at least one lowercase letter (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Password policies are, in part, used to enforce password complexity
requirements. IAM password policies can be used to ensure password are comprised
of different character sets. It is recommended that the password policy require
at least one lowercase letter.

**Rationale:**

Setting a password complexity policy increases account resiliency against brute
force login attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via the AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Requires at least one lowercase letter" is checked under "Password
    Policy"

Via CLI

`aws iam get-account-password-policy`

Ensure the output of the above command includes "RequireLowercaseCharacters":
true

**Remediation:**

Perform the following to set the password policy as prescribed:

Via the AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Requires at least one lowercase letter"

>   Click "Apply password policy"

Via CLI

aws iam update-account-password- --require-lowercase-characters

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.

#### 1.7 Ensure IAM password policy require at least one symbol (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Password policies are, in part, used to enforce password complexity
requirements. IAM password policies can be used to ensure password are comprised
of different character sets. It is recommended that the password policy require
at least one symbol.

**Rationale:**

Setting a password complexity policy increases account resiliency against brute
force login attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Require at least one non-alphanumeric character" is checked under
    "Password Policy"

Via CLI

`aws iam get-account-password-policy`

Ensure the output of the above command includes "RequireSymbols": true

**Remediation:**

Perform the following to set the password policy as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Require at least one non-alphanumeric character"

>   Click "Apply password policy"

Via CLI

`aws iam update-account-password- --require-symbols`
Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.

#### <br>1.8 Ensure IAM password policy require at least one number (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Password policies are, in part, used to enforce password complexity
requirements. IAM password policies can be used to ensure password are comprised
of different character sets. It is recommended that the password policy require
at least one number.

**Rationale:**

Setting a password complexity policy increases account resiliency against brute
force login attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Require at least one number " is checked under "Password Policy"

Via CLI

`aws iam get-account-password-policy`

Ensure the output of the above command includes "RequireNumbers": true

**Remediation:**

Perform the following to set the password policy as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Require at least one number"

5.  Click "Apply password policy"

Via CLI

aws iam update-account-password-policy --require-numbers

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.

#### 1.9 Ensure IAM password policy requires minimum length of 14 or greater (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Password policies are, in part, used to enforce password complexity
requirements. IAM password policies can be used to ensure password are at least
a given length. It is recommended that the password policy require a minimum
password length 14.

**Rationale:**

Setting a password complexity policy increases account resiliency against brute
force login attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Minimum password length" is set to 14 or greater.

Via CLI

`aws iam get-account-password-policy`

Ensure the output of the above command includes "MinimumPasswordLength": 14 (or
higher)

**Remediation:**

Perform the following to set the password policy as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Set "Minimum password length" to 14 or greater.

5.  Click "Apply password policy"

Via CLI

aws iam update-account-password-policy --minimum-password-length 14

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.


#### 1.10 Ensure IAM password policy prevents password reuse (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

IAM password policies can prevent the reuse of a given password by the same
user. It is recommended that the password policy prevent the reuse of passwords.

**Rationale:**

Preventing password reuse increases account resiliency against brute force login
attempts.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Prevent password reuse" is checked

5.  Ensure "Number of passwords to remember" is set to 24

Via CLI

`aws iam get-account-password-policy`

Ensure the output of the above command includes "PasswordReusePrevention": 24

**Remediation:**

Perform the following to set the password policy as prescribed:

Via AWS Console

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Prevent password reuse"

5.  Set "Number of passwords to remember" is set to 24

Via CLI

aws iam update-account-password-policy --password-reuse-prevention 24

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.



4.4 *Use Unique Passwords*

Where multi-factor authentication is not supported (such as local administrator,
root, or service accounts), accounts will use passwords that are unique to that
system.

#### 1.11 Ensure IAM password policy expires passwords within 90 days or less (Scored) 

**Profile Applicability:**

-   Level 1

**Description:**

IAM password policies can require passwords to be rotated or expired after a
given number of days. It is recommended that the password policy expire
passwords after 90 days or less.

**Rationale:**

Reducing the password lifetime increases account resiliency against brute force
login attempts. Additionally, requiring regular password changes help in the
following scenarios:

-   Passwords can be stolen or compromised sometimes without your knowledge.
    This can happen via a system compromise, software vulnerability, or internal
    threat.

-   Certain corporate and government web filters or proxy servers have the
    ability to intercept and record traffic even if it's encrypted.

-   Many people use the same password for many systems such as work, email, and
    personal.

-   Compromised end user workstations might have a keystroke logger.

**Audit:**

Perform the following to ensure the password policy is configured as prescribed:
Via AWS Console:

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Ensure "Enable password expiration" is checked

5.  Ensure "Password expiration period (in days):" is set to 90 or less

Via CLI

aws iam get-account-password-policy

Ensure the output of the above command includes "MaxPasswordAge": 90 or less

**Remediation:**

Perform the following to set the password policy as prescribed: Via AWS Console:

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Go to IAM Service on the AWS Console

3.  Click on Account Settings on the Left Pane

4.  Check "Enable password expiration"

5.  Set "Password expiration period (in days):" to 90 or less

Via CLI

aws iam update-account-password-policy --max-password-age 90

Note: All commands starting with "aws iam update-account-password-policy" can be
combined into a single command.



#### 1.12 Ensure no root account access key exists (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

The root account is the most privileged user in an AWS account. AWS Access Keys
provide programmatic access to a given AWS account. It is recommended that all
access keys associated with the root account be removed.

**Rationale:**

Removing access keys associated with the root account limits vectors by which
the account can be compromised. Additionally, removing the root access keys
encourages the creation and use of role based accounts that are least
privileged.

**Audit:**

Perform the following to determine if the root account has access keys:

Via the AWS Console

1.  Login to the AWS Management Console

2.  Click Services

3.  Click IAM

4.  Click on Credential Report

5.  This will download an .xls file which contains credential usage for all IAM
    users within an AWS Account - open this file

6.  For the \<root_account\> user, ensure the access_key_1_active and
    access_key_2_active fields are set to FALSE .

Via CLI

1.  Run the following commands:

`aws iam generate-credential-report`

`aws iam get-credential-report --query 'Content' --output text \| base64 -d \|
cut -d, -f1,9,14 \| grep -B1 '\<root_account\>'`

1.  For the \<root_account\> user, ensure the access_key_1_active and
    access_key_2_active fields are set to FALSE .

**Remediation:**

Perform the following to delete or disable active root access keys being

Via the AWS Console

1.  Sign in to the AWS Management Console as Root and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  Click on *\<Root_Account_Name\>* at the top right and select Security
    Credentials from the drop down list

3.  On the pop out screen Click on Continue to Security Credentials

4.  Click on Access Keys *(Access Key ID and Secret Access Key)*

5.  Under the Status column if there are any Keys which are Active

    1.  Click on Make Inactive - (Temporarily disable Key - may be needed again)

    2.  Click Delete - (Deleted keys cannot be recovered)

**References:**

1.  [http://docs.aws.amazon.com/general/latest/gr/aws-access-keys-bestpractices.html
    ](http://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html)

2.  [http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html
    ](http://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)

3.  [http://docs.aws.amazon.com/IAM/latest/APIReference/API_GetAccountSummary.
    html
    ](http://docs.aws.amazon.com/IAM/latest/APIReference/API_GetAccountSummary.html)



4.3 *Ensure the Use of Dedicated Administrative Accounts*

Ensure that all users with administrative account access use a dedicated or
secondary account for elevated activities. This account should only be used for
administrative activities and not internet browsing, email, or similar
activities.

#### 1.13 Ensure MFA is enabled for the "root" account (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

The root account is the most privileged user in an AWS account. MFA adds an
extra layer of protection on top of a user name and password. With MFA enabled,
when a user signs in to an AWS website, they will be prompted for their user
name and password as well as for an authentication code from their AWS MFA
device.

**Note:** When virtual MFA is used for root accounts, it is recommended that the
device used is NOT a personal device, but rather a dedicated mobile device
(tablet or phone) that is managed to be kept charged and secured independent of
any individual personal devices. ("non-personal virtual MFA") This lessens the
risks of losing access to the MFA due to device loss, device trade-in or if the
individual owning the device is no longer employed at the company.

**Rationale:**

Enabling MFA provides increased security for console access as it requires the
authenticating principal to possess a device that emits a time-sensitive key and
have knowledge of a credential.

**Audit:**

Perform the following to determine if the root account has MFA setup:

1.  Run the following command:

aws iam get-account-summary \| grep "AccountMFAEnabled"

1.  Ensure the AccountMFAEnabled property is set to 1

**Remediation:**

Perform the following to establish MFA for the root account:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

Note: to manage MFA devices for the root AWS account, you must use your root
account credentials to sign in to AWS. You cannot manage MFA devices for the
root account using other credentials.

1.  Choose Dashboard , and under Security Status , expand Activate MFA on your
    root account.

2.  Choose Activate MFA

3.  In the wizard, choose A virtual MFA device and then choose Next Step .

4.  IAM generates and displays configuration information for the virtual MFA
    device, including a QR code graphic. The graphic is a representation of the
    'secret configuration key' that is available for manual entry on devices
    that do not support QR codes.

5.  Open your virtual MFA application. (For a list of apps that you can use for
    hosting virtual MFA devices, see [Virtual MFA
    Applications.](http://aws.amazon.com/iam/details/mfa/#Virtual_MFA_Applications))
    If the virtual MFA application supports multiple accounts (multiple virtual
    MFA devices), choose the option to create a new account (a new virtual MFA
    device).

6.  Determine whether the MFA app supports QR codes, and then do one of the
    following:

    -   Use the app to scan the QR code. For example, you might choose the
        camera icon or choose an option similar to Scan code, and then use the
        device's camera to scan the code.

    -   In the Manage MFA Device wizard, choose Show secret key for manual
        configuration, and then type the secret configuration key into your MFA
        application.

When you are finished, the virtual MFA device starts generating one-time
passwords.

>   1. In the Manage MFA Device wizard, in the Authentication Code 1 box, type
>   the onetime password that currently appears in the virtual MFA device. Wait
>   up to 30 seconds for the device to generate a new one-time password. Then
>   type the second one-time password into the Authentication Code 2 box. Choose
>   Active Virtual MFA.

#### 1.14 Ensure hardware MFA is enabled for the "root" account (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

The root account is the most privileged user in an AWS account. MFA adds an
extra layer of protection on top of a user name and password. With MFA enabled,
when a user signs in to an AWS website, they will be prompted for their user
name and password as well as for an authentication code from their AWS MFA
device. For Level 2, it is recommended that the root account be protected with a
hardware MFA.

**Rationale:**

A hardware MFA has a smaller attack surface than a virtual MFA. For example, a
hardware MFA does not suffer the attack surface introduced by the mobile
smartphone on which a virtual MFA resides.

**Note**: Using hardware MFA for many, many AWS accounts may create a logistical
device management issue. If this is the case, consider implementing this Level 2
recommendation selectively to the highest security AWS accounts and the Level 1
recommendation applied to the remaining accounts.

Link to order AWS compatible hardware MFA device:
[http://onlinenoram.gemalto.com/ ](http://onlinenoram.gemalto.com/)

**Audit:**

Perform the following to determine if the root account has a hardware MFA setup:

1.  Run the following command to determine if the root account has MFA setup:

aws iam get-account-summary \| grep "AccountMFAEnabled"

The AccountMFAEnabled property is set to 1 will ensure that root account has MFA
(Virtual or Hardware) Enabled.

If AccountMFAEnabled property is set to 0 the account is not compliant with this
recommendation.

1.  If AccountMFAEnabled property is set to 1, determine root account has
    Hardware MFA enabled.

>   Run the following command to list all virtual MFA devices:

aws iam list-virtual-mfa-devices

If the output contains one MFA with the following Serial Number, it means the
MFA is virtual, not hardware and the account is not compliant with this
recommendation:

"SerialNumber":
"arn:aws:iam::_\<aws_account_number\>_:mfa/root-account-mfadevice"

**Remediation:**

Perform the following to establish a hardware MFA for the root account:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

Note: to manage MFA devices for the root AWS account, you must use your root
account credentials to sign in to AWS. You cannot manage MFA devices for the
root account using other credentials.

1.  Choose Dashboard , and under Security Status , expand Activate MFA on your
    root account.

2.  Choose Activate MFA

3.  In the wizard, choose A hardware MFA device and then choose Next Step .

4.  In the Serial Number box, enter the serial number that is found on the back
    of the MFA device.

5.  In the Authentication Code 1 box, enter the six-digit number displayed by
    the MFA device. You might need to press the button on the front of the
    device to display the number. 7. Wait 30 seconds while the device refreshes
    the code, and then enter the next six-digit number into the Authentication
    Code 2 box. You might need to press the button on the front of the device
    again to display the second number.

8. Choose Next Step . The MFA device is now associated with the AWS account. The
next time you use your AWS account credentials to sign in, you must type a code
from the hardware MFA device.

**References:**

1.  Order Hardware MFA: [http://onlinenoram.gemalto.com/
    ](http://onlinenoram.gemalto.com/)

2.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_vir
    tual.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html)

3.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_ph
    ysical.html\#enable-hw-mfa-for-root
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_physical.html#enable-hw-mfa-for-root)

**Notes:** added the CLI for audit based on the output of 'aws iam
list-virtual-mfa-devices'

Remediation should be only through the AWS Console.

#### 1.15 Ensure security questions are registered in the AWS account (Not Scored) 

**Profile Applicability:**

 Level 1

**Description:**

The AWS support portal allows account owners to establish security questions
that can be used to authenticate individuals calling AWS customer service for
support. It is recommended that security questions be established.

**Rationale:**

When creating a new AWS account, a default super user is automatically created.
This account is referred to as the "root" account. It is recommended that the
use of this account be limited and highly controlled. During events in which the
Root password is no longer accessible or the MFA token associated with root is
lost/destroyed it is possible, through authentication using secret questions and
associated answers, to recover root login access.

**Audit:**

Perform the following in the AWS Management Console:

1.  Login to the AWS account as root

2.  On the top right you will see the *\<Root_Account_Name\>*

3.  Click on the *\<Root_Account_Name\>*

4.  From the drop-down menu Click My Account

5.  In the Configure Security Challenge Questions section on the Personal
    Information page, configure three security challenge questions.

6.  Click Save questions .

**Remediation:**

Perform the following in the AWS Management Console:

1.  Login to the AWS Account as root

2.  Click on the *\<Root_Account_Name\>* from the top right of the console

3.  From the drop-down menu Click *My Account*

4.  Scroll down to the Configure Security Questions section

5.  Click on Edit

6.  Click on each Question

-   From the drop-down select an appropriate question

-   Click on the Answer section

-   Enter an appropriate answer o Follow process for all 3 questions

1.  Click Update when complete

2.  Place Questions and Answers and place in a secure physical location

#### 1.16 Ensure IAM policies are attached only to groups or roles (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

By default, IAM users, groups, and roles have no access to AWS resources. IAM
policies are the means by which privileges are granted to users, groups, or
roles. It is recommended that IAM policies be applied directly to groups and
roles but not users.

**Rationale:**

Assigning privileges at the group or role level reduces the complexity of access
management as the number of users grow. Reducing access management complexity
may in-turn reduce opportunity for a principal to inadvertently receive or
retain excessive privileges.

**Audit:**

Perform the following to determine if policies are attached directly to users:

1.  Run the following to get a list of IAM users:

>   aws iam list-users --query 'Users[\*].UserName' --output text

1.  For each user returned, run the following command to determine if any
    policies are attached to them:

>   aws iam list-attached-user-policies --user-name \<iam_user\> aws iam
>   list-user-policies --user-name \<iam_user\>

1.  If any policies are returned, the user has a direct policy attachment.

**Remediation:**

Perform the following to create an IAM group and assign a policy to it:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the navigation pane, click Groups and then click Create New Group .

3.  In the Group Name box, type the name of the group and then click Next Step .

4.  In the list of policies, select the check box for each policy that you want
    to apply to all members of the group. Then click Next Step .

5.  Click Create Group

Perform the following to add a user to a given group:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the navigation pane, click Groups

3.  Select the group to add a user to

4.  Click Add Users To Group

5.  Select the users to be added to the group

6.  Click Add Users

Perform the following to remove a direct association between a user and policy:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the left navigation pane, click on Users

3.  For each user:

    1.  Select the user

    2.  Click on the Permissions tab

    3.  Expand Managed Policies

    4.  Click Detach Policy for each policy

    5.  Expand Inline Policies

    6.  Click Remove Policy for each policy

**References:**

1.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

2.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vsinline.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)

#### 1.17 Maintain current contact details (Not Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Ensure contact email and telephone details for AWS accounts are current and map
to more than one individual in your organization.

An AWS account supports a number of contact details, and AWS will use these to
contact the account owner if activity judged to be in breach of Acceptable Use
Policy or indicative of likely security compromise is observed by the AWS Abuse
team. Contact details should not be for a single individual, as circumstances
may arise where that individual is unavailable. Email contact details should
point to a mail alias which forwards email to multiple individuals within the
organization; where feasible, phone contact details should point to a PABX hunt
group or other call-forwarding system.

**Rationale:**

If an AWS account is observed to be behaving in a prohibited or suspicious
manner, AWS will attempt to contact the account owner by email and phone using
the contact details listed. If this is unsuccessful and the account behavior
needs urgent mitigation, proactive measures may be taken, including throttling
of traffic between the account exhibiting suspicious behavior and the AWS API
endpoints and the Internet. This will result in impaired service to and from the
account in question, so it is in both the customers’ and

AWS’ best interests that prompt contact can be established. This is best
achieved by setting AWS account contact details to point to resources which have
multiple individuals as recipients, such as email aliases and PABX hunt groups.

**Audit:**

This activity can only be performed via the AWS Console, with a user who has
permission to read and write Billing information (aws-portal:\*Billing ).

-   Sign in to the AWS Management Console and open the Billing and Cost
    Management console at https://console.aws.amazon.com/billing/home\#/.

-   On the navigation bar, choose your account name, and then choose My Account.

-   On the Account Settings page, review and verify the current details.

-   Under Contact Information, review and verify the current details.

**Remediation:**

This activity can only be performed via the AWS Console, with a user who has
permission to read and write Billing information (aws-portal:\*Billing ).

-   Sign in to the AWS Management Console and open the Billing and Cost
    Management console at https://console.aws.amazon.com/billing/home\#/.

-   On the navigation bar, choose your account name, and then choose My Account.

-   On the Account Settings page, next to Account Settings, choose Edit.

-   Next to the field that you need to update, choose Edit.

-   After you have entered your changes, choose Save changes.

-   After you have made your changes, choose Done.

-   To edit your contact information, under Contact Information, choose Edit.

-   For the fields that you want to change, type your updated information, and
    then choose Update.

**References:**

>   [1.
>   https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-accountpayment.html\#contact-info
>   ](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/manage-account-payment.html#contact-info)

### 1.18 Ensure security contact information is registered (Not Scored) 

**Profile Applicability:**

 Level 1

**Description:**

AWS provides customers with the option of specifying the contact information for
account's security team. It is recommended that this information be provided.

**Rationale:**

Specifying security-specific contact information will help ensure that security
advisories sent by AWS reach the team in your organization that is best equipped
to respond to them.

**Audit:**

Perform the following in the AWS Management Console to determine if security
contact information is present:

1.  Click on your account name at the top right corner of the console

2.  From the drop-down menu Click My Account

3.  Scroll down to the Alternate Contacts section

4.  Ensure contact information is specified in the Security section

**Remediation:**

Perform the following in the AWS Management Console to establish security
contact information:

1.  Click on your account name at the top right corner of the console.

2.  From the drop-down menu Click My Account

3.  Scroll down to the Alternate Contacts section

4.  Enter contact information in the Security section

Note: Consider specifying an internal email distribution list to ensure emails
are regularly monitored by more than one individual.

### 1.19 Ensure IAM instance roles are used for AWS resource access from 

### instances (Not Scored) 

**Profile Applicability:**

 Level 2

**Description:**

AWS access from within AWS instances can be done by either encoding AWS keys
into AWS API calls or by assigning the instance to a role which has an
appropriate permissions policy for the required access. "AWS Access" means
accessing the APIs of AWS in order to access AWS resources or manage AWS account
resources.

**Rationale:**

AWS IAM roles reduce the risks associated with sharing and rotating credentials
that can be used outside of AWS itself. If credentials are compromised, they can
be used from outside of the AWS account they give access to. In contrast, in
order to leverage role permissions an attacker would need to gain and maintain
access to a specific instance to use the privileges associated with it.

Additionally, if credentials are encoded into compiled applications or other
hard to change mechanisms, then they are even more unlikely to be properly
rotated due to service disruption risks. As time goes on, credentials that
cannot be rotated are more likely to be known by an increasing number of
individuals who no longer work for the organization owning the credentials.

**Audit:**

Whether an Instance Is Associated With a Role

For instances that are known to perform AWS actions, ensure that they belong to
an instance role that has the necessary permissions:

1.  Login to AWS Console (with appropriate permissions to View Identity Access
    Management Account Settings)

2.  Open the EC2 Dashboard and choose "Instances"

3.  Click the EC2 instance that performs AWS actions, in the lower pane details
    find "IAM Role"

4.  If the Role is blank, the instance is not assigned to one.

5.  If the Role is filled in, it does not mean the instance might not \*also\*
    have credentials encoded on it for some activities.

Whether an Instance Contains Embedded Credentials

On the instance that is known to perform AWS actions, audit all scripts and
environment variables to ensure that none of them contain AWS credentials.

Whether an Instance Application Contains Embedded Credentials

Applications that run on an instance may also have credentials embedded. This is
a bad practice, but even worse if the source code is stored in a public code
repository such as github. When an application contains credentials can be
determined by eliminating all other sources of credentials and if the
application can still access AWS resources - it likely contains embedded
credentials. Another method is to examine all source code and configuration
files of the application.

**Remediation:**

IAM roles can only be associated at the launch of an instance. To remediate an
instance to add it to a role you must create a new instance.

If the instance has no external dependencies on its current private ip or public
addresses are elastic IPs:

1.  In AWS IAM create a new role. Assign a permissions policy if needed
    permissions are already known.

2.  In the AWS console launch a new instance with identical settings to the
    existing instance, and ensure that the newly created role is selected.

3.  Shutdown both the existing instance and the new instance.

4.  Detach disks from both instances.

5.  Attach the existing instance disks to the new instance.

6.  Boot the new instance and you should have the same machine, but with the
    associated role.

Note: if your environment has dependencies on a dynamically assigned PRIVATE IP
address you can create an AMI from the existing instance, destroy the old one
and then when launching from the AMI, manually assign the previous private IP
address.

Note: if your environment has dependencies on a dynamically assigned PUBLIC IP
address there is not a way ensure the address is retained and assign an instance
role. Dependencies on dynamically assigned public IP addresses are a bad
practice and, if possible, you may wish to rebuild the instance with a new
elastic IP address and make the investment to remediate affected systems while
assigning the system to a role.

**References:**

1.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-roleec2.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_use_switch-role-ec2.html)

2.  [http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazonec2.html
    ](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/iam-roles-for-amazon-ec2.html)

### 1.20 Ensure a support role has been created to manage incidents with AWS Support (Scored) 

**Profile Applicability:**

-   Level 1

**Description:**

AWS provides a support center that can be used for incident notification and
response, as well as technical support and customer services. Create an IAM Role
to allow authorized users to manage incidents with AWS Support.

**Rationale:**

By implementing least privilege for access control, an IAM Role will require an
appropriate IAM Policy to allow Support Center Access in order to manage
Incidents with AWS Support.

**Audit:**

Using the Amazon unified command line interface:

-   List IAM policies, filter for the 'AWSSupportAccess' managed policy, and
    note the "Arn" element value:

aws iam list-policies --query "Policies[?PolicyName == 'AWSSupportAccess']"

-   Check if the 'AWSSupportAccess' is attached to any IAM user, group or role:

aws iam list-entities-for-policy --policy-arn \<iam_policy_arn\>

**Remediation:**

Using the Amazon unified command line interface:

-   Create an IAM role for managing incidents with AWS:

>   o Create a trust relationship policy document that allows \<iam_user\> to
>   manage AWS incidents, and save it locally as /tmp/TrustPolicy.json:

{

"Version": "2012-10-17",

"Statement": [

{

"Effect": "Allow",

"Principal": {

"AWS": "\<span style="font-style: italic;"\>\<iam_user\>\</span\>"

},

"Action": "sts:AssumeRole"

}

]

}

-   Create the IAM role using the above trust policy:

aws iam create-role --role-name \<aws_support_iam_role\>
--assume-rolepolicy-document file:///tmp/TrustPolicy.json

-   Attach 'AWSSupportAccess' managed policy to the created IAM role:

aws iam attach-role-policy --policy-arn \<iam_policy_arn\> --role-name

\<aws_support_iam_role\>

**Impact:**

All AWS Support plans include an unlimited number of account and billing support
cases, with no long-term contracts. Support billing calculations are performed
on a per-account basis for all plans. Enterprise Support plan customers have the
option to include multiple enabled accounts in an aggregated monthly billing
calculation. Monthly charges for the Business and Enterprise support plans are
based on each month's AWS usage charges, subject to a monthly minimum, billed in
advance.

**References:**

1.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vsinline.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)

2.  [https://aws.amazon.com/premiumsupport/pricing/
    ](https://aws.amazon.com/premiumsupport/pricing/)

3.  [http://docs.aws.amazon.com/cli/latest/reference/iam/list-policies.html
    ](http://docs.aws.amazon.com/cli/latest/reference/iam/list-policies.html)

4.  [http://docs.aws.amazon.com/cli/latest/reference/iam/attach-role-policy.html
    ](http://docs.aws.amazon.com/cli/latest/reference/iam/attach-role-policy.html)

5.  [http://docs.aws.amazon.com/cli/latest/reference/iam/list-entities-for-policy.html
    ](http://docs.aws.amazon.com/cli/latest/reference/iam/list-entities-for-policy.html)

### 1.21 Do not setup access keys during initial user setup for all IAM users that have a console password (Not Scored) 

**Profile Applicability:**

 Level 1

**Description:**

AWS console defaults the checkbox for creating access keys to enabled. This
results in many access keys being generated unnecessarily. In addition to
unnecessary credentials, it also generates unnecessary management work in
auditing and rotating these keys.

**Rationale:**

Requiring that additional steps be taken by the user after their profile has
been created will give a stronger indication of intent that access keys are [a]
necessary for their work and [b] once the access key is established on an
account that the keys may be in use somewhere in the organization.

**Note**: Even if it is known the user will need access keys, require them to
create the keys themselves or put in a support ticket to have the created as a
separate step from user creation.

**Audit:**

Perform the following to determine if access keys are rotated as prescribed:

1.  Login to the AWS Management Console

2.  Click Services 3. Click IAM

3.  Click on a User

4.  Compare the user creation date to the key 1 creation date.

5.  For any that match, the key was created during initial user setup.

>    Keys that were created at the same time as the user profile and do not
>   have a last used date should be deleted.

Via the CLI

1.  Run the following command (OSX/Linux/UNIX) to generate a list of all IAM
    users along with their access keys utilization:

>   aws iam generate-credential-report

>   aws iam get-credential-report --query 'Content' --output text \| base64 -d
>   \| cut -d, -f1,4,9,11,14,16

1.  The output of this command will produce a table similar to the following:

| user,password_enabled,access_key_1_active,access_key_1_last_used_date,access\_ key_2_active,access_key_2_last_used_date elise,false,true,2015-04-16T15:14:00+00:00,false,N/A brandon,true,true,N/A,false,N/A rakesh,false,false,N/A,false,N/A helene,false,true,2015-11-18T17:47:00+00:00,false,N/A paras,true,true,2016-08-28T12:04:00+00:00,true,2016-03-04T10:11:00+00:00 anitha,true,true,2016-06-08T11:43:00+00:00,true,N/A |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|


2.  For any user having access_key_last_used_date set to N/A , ensure that
    access key is deleted .

**Remediation:**

Perform the following to delete access keys that do not pass the audit:

1.  Login to the AWS Management Console:

2.  Click Services

3.  Click IAM

4.  Click on Users

5.  Click on Security Credentials

6.  As an Administrator

>    Click on Delete for keys that were created at the same time as the user
>   profile but have not been used.

>   7. As an IAM User

>    Click on Delete for keys that were created at the same time as the user
>   profile but have not been used.

Via CLI

aws iam delete-access-key

**Notes:**

Credential report does not appear to contain "Key Creation Date" - maybe a
feature request to AWS?

### 1.22 Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

IAM policies are the means by which privileges are granted to users, groups, or
roles. It is recommended and considered a standard security advice to grant
*least privilege*—that is, granting only the permissions required to perform a
task. Determine what users need to do and then craft policies for them that let
the users perform *only* those tasks, instead of allowing full administrative
privileges.

**Rationale:**

It's more secure to start with a minimum set of permissions and grant additional
permissions as necessary, rather than starting with permissions that are too
lenient and then trying to tighten them later.

Providing full administrative privileges instead of restricting to the minimum
set of permissions that the user is required to do exposes the resources to
potentially unwanted actions.

IAM policies that have a statement with "Effect": "Allow" with "Action": "\*"
over "Resource": "\*" should be removed.

**Audit:**

Perform the following to determine what policies are created:

1.  Run the following to get a list of IAM policies:

aws iam list-policies --output text

1.  For each policy returned, run the following command to determine if any
    policies is allowing full administrative privileges on the account:

aws iam get-policy-version --policy-arn \<policy_arn\> --version-id \<version\>

1.  In output ensure policy should not have any Statement block with "Effect":

>   "Allow" and Action set to "\*" and Resource set to "\*"

**Remediation:**

Using the GUI, perform the following to detach the policy that has full
administrative privileges:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam/.](https://console.aws.amazon.com/iam/)

2.  In the navigation pane, click Policies and then search for the policy name
    found in the audit step.

3.  Select the policy that needs to be deleted.

4.  In the policy action menu, select first Detach

5.  Select all Users, Groups, Roles that have this policy attached

6.  Click Detach Policy

7.  In the policy action menu, select Detach

Using the CLI, perform the following to detach the policy that has full
administrative privileges as found in the audit step:

1.  Lists all IAM users, groups, and roles that the specified managed policy is
    attached to.

aws iam list-entities-for-policy --policy-arn \<policy_arn\>

1.  Detach the policy from all IAM Users:

aws iam detach-user-policy --user-name \<iam_user\> --policy-arn \<policy_arn\>

1.  Detach the policy from all IAM Groups:

aws iam detach-group-policy --group-name \<iam_group\> --policy-arn

\<policy_arn\>

1.  Detach the policy from all IAM Roles:

>   aws iam detach-role-policy --role-name \<iam_role\> --policy-arn
>   \<policy_arn\>

**References:**

1.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)

2.  [http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vsinline.html
    ](http://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_managed-vs-inline.html)

3.  [http://docs.aws.amazon.com/cli/latest/reference/iam/index.html\#cli-aws-iam
    ](http://docs.aws.amazon.com/cli/latest/reference/iam/index.html#cli-aws-iam)

*2 Logging* 
============

This section contains recommendations for configuring AWS's account logging
features.

### 2.1 Ensure CloudTrail is enabled in all regions (Scored) 

**Profile Applicability:**

-   Level 1

**Description:**

AWS CloudTrail is a web service that records AWS API calls for your account and
delivers log files to you. The recorded information includes the identity of the
API caller, the time of the API call, the source IP address of the API caller,
the request parameters, and the response elements returned by the AWS service.
CloudTrail provides a history of AWS API calls for an account, including API
calls made via the Management Console, SDKs, command line tools, and
higher-level AWS services (such as CloudFormation).

**Rationale:**

The AWS API call history produced by CloudTrail enables security analysis,
resource change tracking, and compliance auditing. Additionally,

-   ensuring that a multi-regions trail exists will ensure that unexpected
    activity occurring in otherwise unused regions is detected

-   ensuring that a multi-regions trail exists will ensure that Global Service
    Logging is enabled for a trail by default to capture recording of events
    generated on AWS global services

-   for a multi-regions trail, ensuring that management events configured for
    all type of Read/Writes ensures recording of management operations that are
    performed on all resources in an AWS account

**Audit:**

Perform the following to determine if CloudTrail is enabled for all regions:

Via the management Console

1.  Sign in to the AWS Management Console and open the CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  Click on Trails on the left navigation pane

 You will be presented with a list of trails across all regions

1.  Ensure at least one Trail has All specified in the Region column

2.  Click on a trail via the link in the *Name* column

3.  Ensure Logging is set to ON

4.  Ensure Apply trail to all regions is set to Yes

5.  In section Management Events ensure Read/Write Events set to ALL

Via CLI

aws cloudtrail describe-trails

Ensure IsMultiRegionTrail is set to true

aws cloudtrail get-trail-status --name \<trailname shown in describe-trails\>

Ensure IsLogging is set to true

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

**Remediation:**

Perform the following to enable global (Multi-region) CloudTrail logging:

Via the management Console

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  Click on *Trails* on the left navigation pane

3.  Click Get Started Now , if presented

-   Click Add new trail

-   Enter a trail name in the Trail name box

-   Set the Apply trail to all regions option to Yes

-   Specify an S3 bucket name in the S3 bucket box

-   Click Create

1.  If 1 or more trails already exist, select the target trail to enable for
    global logging

2.  Click the edit icon (pencil) next to Apply trail to all regions , Click Yes
    and Click Save.

3.  Click the edit icon (pencil) next to Management Events click All for setting
    Read/Write Events and Click Save.

Via CLI

aws cloudtrail create-trail --name \<trail_name\> --bucket-name
\<s3_bucket_for_cloudtrail\> --is-multi-region-trail

aws cloudtrail update-trail --name \<trail_name\> --is-multi-region-trail

Note: Creating CloudTrail via CLI without providing any overriding options
configures Management Events to set All type of Read/Writes by default.

**Impact:**

**TODO: Setup S3 lifecycle features**

S3 lifecycle features can be used to manage the accumulation and management of
logs over time. See the following AWS resource for more information on these
features:

>   1. http://docs.aws.amazon.com/AmazonS3/latest/dev/object-lifecycle-mgmt.html

**Default Value:**

Not Enabled

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrailconcepts.html\#cloudtrail-concepts-management-events
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-concepts.html#cloudtrail-concepts-management-events)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/loggingmanagement-and-data-events-with-](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-management-and-data-events-with-cloudtrail.html?icmpid=docs_cloudtrail_console#logging-management-events)

>   [cloudtrail.html?icmpid=docs_cloudtrail_console\#logging-management-events
>   ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-management-and-data-events-with-cloudtrail.html?icmpid=docs_cloudtrail_console#logging-management-events)

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrailsupported-services.html\#cloud-trail-supported-services-data-events
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-supported-services.html#cloud-trail-supported-services-data-events)

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

### 2.2 Ensure CloudTrail log file validation is enabled (Scored) 

**Profile Applicability:**

-   Level 2

**Description:**

CloudTrail log file validation creates a digitally signed digest file containing
a hash of each log that CloudTrail writes to S3. These digest files can be used
to determine whether a log file was changed, deleted, or unchanged after
CloudTrail delivered the log. It is recommended that file validation be enabled
on all CloudTrails.

**Rationale:**

Enabling log file validation will provide additional integrity checking of
CloudTrail logs.

**Audit:**

Perform the following on each trail to determine if log file validation is
enabled:

Via the management Console

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  Click on Trails on the left navigation pane 3. For Every Trail:

-   Click on a trail via the link in the *Name* column

-   Under the S3 section, ensure Enable log file validation is set to Yes

Via CLI

aws cloudtrail describe-trails

Ensure LogFileValidationEnabled is set to true for each trail **Remediation:**

Perform the following to enable log file validation on a given trail:

Via the management Console

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  Click on Trails on the left navigation pane

3.  Click on target trail

4.  Within the S3 section click on the edit icon (pencil)

5.  Click Advanced

6.  Click on the Yes radio button in section Enable log file validation

7.  Click Save

Via CLI

aws cloudtrail update-trail --name \<trail_name\> --enable-log-file-validation

Note that periodic validation of logs using these digests can be performed by
running the following command:

aws cloudtrail validate-logs --trail-arn \<trail_arn\> --start-time

\<start_time\> --end-time \<end_time\>

**Default Value:**

Not Enabled

**References:**

1.  [http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-filevalidation-enabling.html
    ](http://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudtrail-log-file-validation-enabling.html)

**CIS Controls:**

6 *Maintenance, Monitoring and Analysis of Audit Logs*

Maintenance, Monitoring and Analysis of Audit Logs

### 2.3 Ensure the S3 bucket used to store CloudTrail logs is not publicly 

### accessible (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

CloudTrail logs a record of every API call made in your AWS account. These logs
file are stored in an S3 bucket. It is recommended that the bucket policy, or
access control list (ACL), applied to the S3 bucket that CloudTrail logs to
prevents public access to the CloudTrail logs.

**Rationale:**

Allowing public access to CloudTrail log content may aid an adversary in
identifying weaknesses in the affected account's use or configuration.

**Audit:**

Perform the following to determine if any public access is granted to an S3
bucket via an ACL or S3 bucket policy:

Via the Management Console

1.  Go to the Amazon CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail/home
    ](https://console.aws.amazon.com/cloudtrail/home)

2.  In the API activity history pane on the left, click Trails

3.  In the Trails pane, note the bucket names in the S3 bucket column

4.  Go to Amazon S3 console at <https://console.aws.amazon.com/s3/home> 5. For
    each bucket noted in step 3, right-click on the bucket and click Properties

5.  In the Properties pane, click the Permissions tab.

6.  The tab shows a list of grants, one row per grant, in the bucket ACL. Each
    row identifies the grantee and the permissions granted.

7.  Ensure no rows exists that have the Grantee set to Everyone or the Grantee
    set to Any Authenticated User.

8.  If the Edit bucket policy button is present, click it to review the bucket
    policy.

9.  Ensure the policy does not contain a Statement having an Effect set to Allow
    and a Principal set to "\*" or {"AWS" : "\*"}

Via CLI:

1.  Get the name of the S3 bucket that CloudTrail is logging to:

>   aws cloudtrail describe-trails --query 'trailList[\*].S3BucketName'

1.  Ensure the AllUsers principal is not granted privileges to that \<bucket\> :

aws s3api get-bucket-acl --bucket \<s3_bucket_for_cloudtrail\> --query
'Grants[?Grantee.URI== \`http://acs.amazonaws.com/groups/global/AllUsers\` ]'

1.  Ensure the AuthenticatedUsers principal is not granted privileges to that
    \<bucket\>

>   :

aws s3api get-bucket-acl --bucket \<s3_bucket_for_cloudtrail\> --query
'Grants[?Grantee.URI== \`http://acs.amazonaws.com/groups/global/Authenticated
Users\` ]'

1.  Get the S3 Bucket Policy

>   aws s3api get-bucket-policy --bucket \<s3_bucket_for_cloudtrail\>

1.  Ensure the policy does not contain a Statement having an Effect set to Allow
    and a Principal set to "\*" or {"AWS" : "\*"}

Note: Principal set to "\*" or {"AWS" : "\*"} allows anonymous access.

**Remediation:**

Perform the following to remove any public access that has been granted to the
bucket via an ACL or S3 bucket policy:

1.  Go to Amazon S3 console at [https://console.aws.amazon.com/s3/home
    ](https://console.aws.amazon.com/s3/home)

2.  Right-click on the bucket and click Properties

3.  In the Properties pane, click the Permissions tab.

4.  The tab shows a list of grants, one row per grant, in the bucket ACL. Each
    row identifies the grantee and the permissions granted.

5.  Select the row that grants permission to Everyone or Any Authenticated User

6.  Uncheck all the permissions granted to Everyone or Any Authenticated User
    (click x to delete the row).

7.  Click Save to save the ACL.

8.  If the Edit bucket policy button is present, click it.

9.  Remove any Statement having an Effect set to Allow and a Principal set to
    "\*" or {"AWS" : "\*"}.

**Default Value:**

By default, S3 buckets are not publicly accessible

**References:**

1.  [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements\_
    principal.html
    ](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html)

**CIS Controls:**

14.6 *Protect Information through Access Control Lists*

Protect all information stored on systems with file system, network share,
claims, application, or database specific access control lists. These controls
will enforce the principle that only authorized individuals should have access
to the information based on their need to access the information as a part of
their responsibilities.

### 2.4 Ensure CloudTrail trails are integrated with CloudWatch Logs (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

AWS CloudTrail is a web service that records AWS API calls made in a given AWS
account. The recorded information includes the identity of the API caller, the
time of the API call, the source IP address of the API caller, the request
parameters, and the response elements returned by the AWS service. CloudTrail
uses Amazon S3 for log file storage and delivery, so log files are stored
durably. In addition to capturing CloudTrail logs within a specified S3 bucket
for long term analysis, realtime analysis can be performed by configuring
CloudTrail to send logs to CloudWatch Logs. For a trail that is enabled in all
regions in an account, CloudTrail sends log files from all those regions to a
CloudWatch Logs log group. It is recommended that CloudTrail logs be sent to
CloudWatch Logs.

Note: The intent of this recommendation is to ensure AWS account activity is
being captured, monitored, and appropriately alarmed on. CloudWatch Logs is a
native way to accomplish this using AWS services but does not preclude the use
of an alternate solution.

**Rationale:**

Sending CloudTrail logs to CloudWatch Logs will facilitate real-time and
historic activity logging based on user, API, resource, and IP address, and
provides opportunity to establish alarms and notifications for anomalous or
sensitivity account activity.

**Audit:**

Perform the following to ensure CloudTrail is configured as prescribed:

Via the AWS management Console

1.  Sign in to the AWS Management Console and open the CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail/
    ](https://console.aws.amazon.com/cloudtrail/)

2.  Under All Buckets , click on the target bucket you wish to evaluate

3.  Click Properties on the top right of the console

4.  Click Trails in the left menu

5.  Ensure a CloudWatch Logs log group is configured and has a recent (\~one day
    old) Last log file delivered timestamp.

Via CLI

1.  Run the following command to get a listing of existing trails:

>   aws cloudtrail describe-trails

1.  Ensure CloudWatchLogsLogGroupArn is not empty and note the value of the Name
    property.

2.  Using the noted value of the Name property, run the following command:

>   aws cloudtrail get-trail-status --name \<trail_name\>

1.  Ensure the LatestcloudwatchLogdDeliveryTime property is set to a recent
    (\~one day old) timestamp.

**Remediation:**

Perform the following to establish the prescribed state:

Via the AWS management Console

1.  Sign in to the AWS Management Console and open the CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail/
    ](https://console.aws.amazon.com/cloudtrail/)

2.  Under All Buckets, click on the target bucket you wish to evaluate

3.  Click Properties on the top right of the console

4.  Click Trails in the left menu

5.  Click on each trail where no CloudWatch Logs are defined

6.  Go to the CloudWatch Logs section and click on Configure

7.  Define a new or select an existing log group

8.  Click on Continue

9.  Configure IAM Role which will deliver CloudTrail events to CloudWatch Logs o
    Create/Select an IAM Role and Policy Name o Click Allow to continue

Via CLI

aws cloudtrail update-trail --name \<trail_name\> --cloudwatch-logs-log-grouparn
\<cloudtrail_log_group_arn\> --cloudwatch-logs-role-arn

\<cloudtrail_cloudwatchLogs_role_arn\>

**Impact:**

Note: By default, CloudWatch Logs will store Logs indefinitely unless a specific
retention period is defined for the log group. When choosing the number of days
to retain, keep in mind the average days it takes an organization to realize
they have been breached is 210 days (at the time of this writing). Since
additional time is required to research a breach, a minimum 365 day retention
policy allows time for detection and research. You may also wish to archive the
logs to a cheaper storage service rather than simply deleting them. See the
following AWS resource to manage CloudWatch Logs retention periods:

>   1.
>   http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/SettingL
>   ogRetention.html

**References:**

1.  [https://aws.amazon.com/cloudtrail/ ](https://aws.amazon.com/cloudtrail/)

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

6.5 *Central Log Management*

Ensure that appropriate logs are being aggregated to a central log management
system for analysis and review.

### 2.5 Ensure AWS Config is enabled in all regions (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

AWS Config is a web service that performs configuration management of supported
AWS resources within your account and delivers log files to you. The recorded
information includes the configuration item (AWS resource), relationships
between configuration items (AWS resources), any configuration changes between
resources. It is recommended to enable AWS Config be enabled in all regions.

**Rationale:**

The AWS configuration item history captured by AWS Config enables security
analysis, resource change tracking, and compliance auditing.

**Audit:**

Process to evaluate AWS Config configuration per region Via AWS Management
Console:

1.  Sign in to the AWS Management Console and open the AWS Config console at
    [https://console.aws.amazon.com/config/.](https://console.aws.amazon.com/config/)

2.  On the top right of the console select target Region.

3.  If presented with Setup AWS Config - follow remediation procedure:

4.  On the Resource inventory page, Click on edit (the gear icon). The Set Up
    AWS Config page appears.

5.  Ensure 1 or both check-boxes under "All Resources" is checked.

>    Include global resources related to IAM resources - which needs to be
>   enabled in 1 region only

1.  Ensure the correct S3 bucket has been defined.

2.  Ensure the correct SNS topic has been defined.

3.  Repeat steps 2 to 7 for each region.

Via AWS Command Line Interface:

1.  Run this command to show all AWS Config recorders and their properties:

aws configservice describe-configuration-recorders

1.  Evaluate the output to ensure that there's at least one recorder for which
    recordingGroup object includes "allSupported": true AND

>   "includeGlobalResourceTypes": true

Note: There is one more parameter "ResourceTypes" in recordingGroup object. We
don't need to check the same as whenever we set "allSupported": true, AWS
enforces resource types to be empty ("ResourceTypes":[]) Sample Output:

| { "ConfigurationRecorders": [ { "recordingGroup": { "allSupported": true, "resourceTypes": [], "includeGlobalResourceTypes": true }, "roleARN": "arn:aws:iam::\<AWS_Account_ID\>:role/servicerole/\<config-role-name\>", "name": "default" } ] } |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|


1.  Run this command to show the status for all AWS Config recorders:

aws configservice describe-configuration-recorder-status

1.  In the output, find recorders with name key matching the recorders that met
    criteria in step 2. Ensure that at least one of them includes "recording":
    true and "lastStatus": "SUCCESS"

**Remediation:**

To implement AWS Config configuration: Via AWS Management Console:

1.  Select the region you want to focus on in the top right of the console

2.  Click Services

3.  Click Config

4.  Define which resources you want to record in the selected region

5.  Choose to include global resources (IAM resources)

6.  Specify an S3 bucket in the same account or in another managed AWS account

7.  Create an SNS Topic from the same AWS account or another managed AWS account

Via AWS Command Line Interface:

1.  Ensure there is an appropriate S3 bucket, SNS topic, and IAM role per the
    [AWS Config Service
    prerequisites.](http://docs.aws.amazon.com/config/latest/developerguide/gs-cli-prereq.html)

2.  Run this command to set up the configuration recorder

aws configservice subscribe --s3-bucket my-config-bucket --sns-topic
arn:aws:sns:us-east-1:012345678912:my-config-notice --iam-role
arn:aws:iam::012345678912:role/myConfigRole

1.  Run this command to start the configuration recorder:

start-configuration-recorder --configuration-recorder-name \<value\>

**References:**

1.  [http://docs.aws.amazon.com/cli/latest/reference/configservice/describeconfiguration-recorder-status.html
    ](http://docs.aws.amazon.com/cli/latest/reference/configservice/describe-configuration-recorder-status.html)

**CIS Controls:**

1.4 *Maintain Detailed Asset Inventory*

Maintain an accurate and up-to-date inventory of all technology assets with the
potential to store or process information. This inventory shall include all
hardware assets, whether connected to the organization's network or not.

11.2 *Document Traffic Configuration Rules*

All configuration rules that allow traffic to flow through network devices
should be documented in a configuration management system with a specific
business reason for each rule, a specific individual’s name responsible for that
business need, and an expected duration of the need.

16.1 *Maintain an Inventory of Authentication Systems*

Maintain an inventory of each of the organization's authentication systems,
including those located onsite or at a remote service provider.

.

### 2.6 Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

S3 Bucket Access Logging generates a log that contains access records for each
request made to your S3 bucket. An access log record contains details about the
request, such as the request type, the resources specified in the request
worked, and the time and date the request was processed. It is recommended that
bucket access logging be enabled on the CloudTrail S3 bucket.

**Rationale:**

By enabling S3 bucket logging on target S3 buckets, it is possible to capture
all events which may affect objects within an target buckets. Configuring logs
to be placed in a separate bucket allows access to log information which can be
useful in security and incident response workflows.

**Audit:**

Perform the following ensure the CloudTrail S3 bucket has access logging is
enabled:

Via the management Console

1.  Go to the Amazon CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail/home
    ](https://console.aws.amazon.com/cloudtrail/home)

2.  In the API activity history pane on the left, click Trails

3.  In the Trails pane, note the bucket names in the S3 bucket column

4.  Sign in to the AWS Management Console and open the S3 console at
    [https://console.aws.amazon.com/s3.](https://console.aws.amazon.com/s3)

5.  Under All Buckets click on a target S3 bucket

6.  Click on Properties in the top right of the console

7.  Under Bucket: \_ \<bucket_name\> \_ click on Logging 8. Ensure Enabled is
    checked.

Via CLI

1.  Get the name of the S3 bucket that CloudTrail is logging to:

aws cloudtrail describe-trails --query 'trailList[\*].S3BucketName'

1.  Ensure Bucket Logging is enabled:

aws s3api get-bucket-logging --bucket \<s3_bucket_for_cloudtrail\>

Ensure command does not returns empty output.

Sample Output for a bucket with logging enabled:

{

"LoggingEnabled": {

"TargetPrefix": "\<Prefix_Test\>",

"TargetBucket": "\<Bucket_name_for_Storing_Logs\>"

} }

**Remediation:**

Perform the following to enable S3 bucket logging:

Via the Management Console

1.  Sign in to the AWS Management Console and open the S3 console at
    [https://console.aws.amazon.com/s3.](https://console.aws.amazon.com/s3)

2.  Under All Buckets click on the target S3 bucket

3.  Click on Properties in the top right of the console

4.  Under Bucket: \<s3_bucket_for_cloudtrail\> click on Logging

5.  Configure bucket logging

    1.  Click on Enabled checkbox

    2.  Select Target Bucket from list

    3.  Enter a Target Prefix

6.  Click Save **Default Value:**

Logging is disabled.

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

14.9 *Enforce Detail Logging for Access or Changes to Sensitive Data*

Enforce detailed audit logging for access to sensitive data or changes to
sensitive data (utilizing tools such as File Integrity Monitoring or Security
Information and Event Monitoring).

### 2.7 Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

AWS CloudTrail is a web service that records AWS API calls for an account and
makes those logs available to users and resources in accordance with IAM
policies. AWS Key Management Service (KMS) is a managed service that helps
create and control the encryption keys used to encrypt account data, and uses
Hardware Security Modules (HSMs) to protect the security of encryption keys.
CloudTrail logs can be configured to leverage server side encryption (SSE) and
KMS customer created master keys (CMK) to further protect CloudTrail logs. It is
recommended that CloudTrail be configured to use SSE-KMS.

**Rationale:**

Configuring CloudTrail to use SSE-KMS provides additional confidentiality
controls on log data as a given user must have S3 read permission on the
corresponding log bucket and must be granted decrypt permission by the CMK
policy.

**Audit:**

Perform the following to determine if CloudTrail is configured to use SSE-KMS:

Via the Management Console

1.  Sign in to the AWS Management Console and open the CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  In the left navigation pane, choose Trails .

3.  Select a Trail

4.  Under the S3 section, ensure Encrypt log files is set to Yes and a KMS key
    ID is specified in the KSM Key Id field.

Via CLI

1.  Run the following command:

aws cloudtrail describe-trails

1.  For each trail listed, SSE-KMS is enabled if the trail has a KmsKeyId
    property defined.

**Remediation:**

Perform the following to configure CloudTrail to use SSE-KMS:

Via the Management Console

1.  Sign in to the AWS Management Console and open the CloudTrail console at
    [https://console.aws.amazon.com/cloudtrail
    ](https://console.aws.amazon.com/cloudtrail)

2.  In the left navigation pane, choose Trails .

3.  Click on a Trail

4.  Under the S3 section click on the edit button (pencil icon)

5.  Click Advanced

6.  Select an existing CMK from the KMS key Id drop-down menu

-   Note: Ensure the CMK is located in the same region as the S3 bucket

-   Note: You will need to apply a KMS Key policy on the selected CMK in order
    for CloudTrail as a service to encrypt and decrypt log files using the CMK
    provided.

>   Steps are provided
>   [here](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/create-kms-key-policy-for-cloudtrail.html)
>   for editing the selected CMK Key policy

1.  Click Save

2.  You will see a notification message stating that you need to have decrypt
    permissions on the specified KMS key to decrypt log files.

3.  Click Yes

Via CLI

aws cloudtrail update-trail --name \<trail_name\> --kms-id

\<cloudtrail_kms_key\>

aws kms put-key-policy --key-id \<cloudtrail_kms_key\> --policy

\<cloudtrail_kms_key_policy\>

**Impact:**

Customer created keys incur an additional cost. See
https://aws.amazon.com/kms/pricing/ for more information.

**References:**

1.  CIS CSC v6.0 \#13.1: Perform an assessment of data to identify sensitive
    information.

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encryptingcloudtrail-log-files-with-aws-kms.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/encrypting-cloudtrail-log-files-with-aws-kms.html)

3.  [http://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html
    ](http://docs.aws.amazon.com/kms/latest/developerguide/create-keys.html)

4.  CIS CSC v6.0 \#6: Maintenance, Monitoring, and Analysis of Audit Logs 5.
    CCE-78919-8

**Notes:**

3 statements which need to be added to the CMK policy:

1.  Enable Cloudtrail to describe CMK properties

\<pre class="programlisting" style="font-style: normal;"\>{

"Sid": "Allow CloudTrail access",

"Effect": "Allow",

"Principal": {

"Service": "cloudtrail.amazonaws.com"

},

"Action": "kms:DescribeKey",

"Resource": "\*"

}

1.  Granting encrypt permissions

\<pre class="programlisting" style="font-style: normal;"\>{

"Sid": "Allow CloudTrail to encrypt logs",

"Effect": "Allow",

"Principal": {

"Service": "cloudtrail.amazonaws.com"

},

"Action": "kms:GenerateDataKey\*",

"Resource": "\*",

"Condition": {

"StringLike": {

"kms:EncryptionContext:aws:cloudtrail:arn": [
"arn:aws:cloudtrail:\*:aws-account-id:trail/\*"

]

}

}

}

3. Granting decrypt permissions

\<pre class="programlisting" style="font-style: normal;"\>{

"Sid": "Enable CloudTrail log decrypt permissions",

"Effect": "Allow",

"Principal": {

"AWS": "arn:aws:iam::aws-account-id:user/username"

},

"Action": "kms:Decrypt",

"Resource": "\*",

"Condition": {

"Null": {

"kms:EncryptionContext:aws:cloudtrail:arn": "false"

}

} }

**CIS Controls:**

6 *Maintenance, Monitoring and Analysis of Audit Logs*

Maintenance, Monitoring and Analysis of Audit Logs

### 2.8 Ensure rotation for customer created CMKs is enabled (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

AWS Key Management Service (KMS) allows customers to rotate the backing key
which is key material stored within the KMS which is tied to the key ID of the
Customer Created customer master key (CMK). It is the backing key that is used
to perform cryptographic operations such as encryption and decryption. Automated
key rotation currently retains all prior backing keys so that decryption of
encrypted data can take place transparently. It is recommended that CMK key
rotation be enabled.

**Rationale:**

Rotating encryption keys helps reduce the potential impact of a compromised key
as data encrypted with a new key cannot be accessed with a previous key that may
have been exposed.

**Audit:**

Via the Management Console:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam.](https://console.aws.amazon.com/iam)

2.  In the left navigation pane, choose Encryption Keys .

3.  Select a customer created master key (CMK)

4.  Under the Key Policy section, move down to Key Rotation *.*

5.  Ensure the Rotate this key every year checkbox is checked.

Via CLI

1.  Run the following command to get a list of all keys and their associated
    KeyIds

aws kms list-keys

1.  For each key, note the KeyId and run the following command

aws kms get-key-rotation-status --key-id \<kms_key_id\>

1.  Ensure KeyRotationEnabled is set to true

**Remediation:**

Via the Management Console:

1.  Sign in to the AWS Management Console and open the IAM console at
    [https://console.aws.amazon.com/iam.](https://console.aws.amazon.com/iam)

2.  In the left navigation pane, choose Encryption Keys .

3.  Select a customer created master key (CMK)

4.  Under the Key Policy section, move down to Key Rotation *.*

5.  Check the Rotate this key every year checkbox.

Via CLI

>   1. Run the following command to enable key rotation:

aws kms enable-key-rotation --key-id \<kms_key_id\>

**References:**

1.  [https://aws.amazon.com/kms/pricing/ ](https://aws.amazon.com/kms/pricing/)

2.  [http://csrc.nist.gov/publications/nistpubs/800-57/sp800-](http://csrc.nist.gov/publications/nistpubs/800-57/sp800-57_part1_rev3_general.pdf)

>   [57_part1_rev3_general.pdf
>   ](http://csrc.nist.gov/publications/nistpubs/800-57/sp800-57_part1_rev3_general.pdf)

1.  CCE-78920-6

**CIS Controls:**

6 *Maintenance, Monitoring and Analysis of Audit Logs*

Maintenance, Monitoring and Analysis of Audit Logs

### 2.9 Ensure VPC flow logging is enabled in all VPCs (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

VPC Flow Logs is a feature that enables you to capture information about the IP
traffic going to and from network interfaces in your VPC. After you've created a
flow log, you can view and retrieve its data in Amazon CloudWatch Logs. It is
recommended that VPC Flow Logs be enabled for packet "Rejects" for VPCs.

**Rationale:**

VPC Flow Logs provide visibility into network traffic that traverses the VPC and
can be used to detect anomalous traffic or insight during security workflows.

**Audit:**

Perform the following to determine if VPC Flow logs is enabled: Via the
Management Console:

1.  Sign into the management console

2.  Select Services then VPC

3.  In the left navigation pane, select Your VPCs

4.  Select a VPC

5.  In the right pane, select the Flow Logs tab.

6.  Ensure a Log Flow exists that has Active in the Status column.

**Remediation:**

Perform the following to determine if VPC Flow logs is enabled: Via the
Management Console:

1.  Sign into the management console

2.  Select Services then VPC

3.  In the left navigation pane, select Your VPCs

4.  Select a VPC

5.  In the right pane, select the Flow Logs tab.

6.  If no Flow Log exists, click Create Flow Log

7.  For Filter, select Reject

8.  Enter in a Role and Destination Log Group

9.  Click Create Log Flow

10. Click on CloudWatch Logs Group

**Note:** Setting the filter to "Reject" will dramatically reduce the logging
data accumulation for this recommendation and provide sufficient information for
the purposes of breach detection, research and remediation. However, during
periods of least privilege security group engineering, setting this the filter
to "All" can be very helpful in discovering existing traffic flows required for
proper operation of an already running environment.

**Impact:**

By default, CloudWatch Logs will store Logs indefinitely unless a specific
retention period is defined for the log group. When choosing the number of days
to retain, keep in mind the average days it takes an organization to realize
they have been breached is 210 days (at the time of this writing). Since
additional time is required to research a breach, a minimum 365 day retention
policy allows time for detection and research. You may also wish to archive the
logs to a cheaper storage service rather than simply deleting them. See the
following AWS resource to manage CloudWatch Logs retention periods:

>   1.
>   http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/SettingL
>   ogRetention.html

**References:**

1.  CCE-79202-8

2.  CIS CSC v6.0 \#6.5, \#12.9

3.  [http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html
    ](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/flow-logs.html)

**Notes:**

Changed title from

"Ensure VPC flow logging is enabled in all applicable regions" to

"Ensure VPC flow logging is enabled in all VPCs"

For these reasons:

1.  Flow logs cannot be enabled for regions, only for VPCs

2.  The statement did not define an "Applicable Region" and did not clarify "all
    VPCs in applicable regions"

3.  All other benchmark recommendations appear to assume that you apply them
    "any actively used configuration or resource" or "All resources" - so
    specifying

>   "applicable" to mean "active" or "compliant with the benchmark" seems
>   unnecessary.

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

12.5 *Configure Monitoring Systems to Record Network Packets*

Configure monitoring systems to record network packets passing through the
boundary at each of the organization's network boundaries.

*3 Monitoring* 
===============

For effectiveness and coverage of recommended metric-filters and alarms,
recommendations in Section 3 should be implemented on Multi-region CloudTrail
referred in Ensure CloudTrail is enabled in all regions Updated Overview should
look like: This section contains recommendations for configuring AWS to assist
with monitoring and responding to account activities. Metric filter-related
recommendations in this section are dependent on the Ensure CloudTrail is
enabled in all regions and Ensure CloudTrail trails are integrated with
CloudWatch Logs recommendation in the "Logging" section. Additionally, step 3 of
the remediation procedure for the same recommendations provides guidance for
establishing an email-based subscription (-protocol email). This is provided as
an example and is not meant to suggest other protocols provide lesser value.

### 3.1 Ensure a log metric filter and alarm exist for unauthorized API calls (Scored) 

<https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CountingLogEventsExample.html>

**Profile Applicability:**

-   Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for unauthorized
API calls.

**Rationale:**

Monitoring unauthorized API calls will help reveal application errors and may
reduce time to detect malicious activity.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.errorCode = "\*UnauthorizedOperation") \|\|
(\$.errorCode

= "AccessDenied\*") }"

1.  Note the \<unauthorized_api_calls_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<unauthorized_api_calls_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<unauthorized_api_calls_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    unauthorized API calls and the \<cloudtrail_log_group_name\> taken from
    audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<unauthorized_api_calls_metric\>\` --metric-transformations
metricName= \`\<unauthorized_api_calls_metric\>\`
,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.errorCode = "\*UnauthorizedOperation") \|\| (\$.errorCode =
"AccessDenied\*") }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name
\`\<unauthorized_api_calls_alarm\>\` --metric-name

\`\<unauthorized_api_calls_metric\>\` --statistic Sum --period 300 --threshold 1

\--comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1
-namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**Impact:**

This alert may be triggered by normal read-only console activities that attempt
to opportunistically gather optional information, but gracefully fail if they
don't have permissions.

If an excessive number of alerts are being generated then an organization may
wish to consider adding read access to the limited IAM user permissions simply
to quiet the alerts.

In some cases doing this may allow the users to actually view some areas of the
system - any additional access given should be reviewed for alignment with the
original limited IAM user intent.

**References:**

1.  [https://aws.amazon.com/sns/ ](https://aws.amazon.com/sns/)

2.  CCE-79186-3

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

4.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

5.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

6.5 *Central Log Management*

Ensure that appropriate logs are being aggregated to a central log management
system for analysis and review.

6.7 *Regularly Review Logs*

On a regular basis, review logs to identify anomalies or abnormal events.

### 3.2 Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for console logins
that are not protected by multi-factor authentication (MFA).

**Rationale:**

Monitoring for single-factor console logins will increase visibility into
accounts that are not protected by MFA.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events aws
    cloudtrail get-event-selectors --trail-name \<trailname shown in
    describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = "ConsoleLogin") &&

(\$.additionalEventData.MFAUsed != "Yes") }"

1.  Note the \<no_mfa_console_signin_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the
    \<no_mfa_console_signin_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<no_mfa_console_signin_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for AWS
    Management Console sign-in without MFA and the \<cloudtrail_log_group_name\>
    taken from audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<no_mfa_console_signin_metric\>\` --metric-transformations
metricName= \`\<no_mfa_console_signin_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = "ConsoleLogin") && (\$.additionalEventData.MFAUsed != "Yes") }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<no_mfa_console_signin_alarm\>\`

\--metric-name \`\<no_mfa_console_signin_metric\>\` --statistic Sum --period 300

\--threshold 1 --comparison-operator GreaterThanOrEqualToThreshold
-evaluation-periods 1 --namespace ‘MIBenchmark’ --alarm-actions

\<sns_topic_arn\>

**References:**

1.  [http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/viewing
    \_metrics_with_cloudwatch.html
    ](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/viewing_metrics_with_cloudwatch.html)

2.  CCE-79187-1

3.  CIS CSC v6.0 \#5.5

4.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

5.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

6.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

16 *Account Monitoring and Control*

Account Monitoring and Control

### 3.3 Ensure a log metric filter and alarm exist for usage of "root" account (Scored) 

**Profile Applicability:**

-   Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for root login
attempts.

**Rationale:**

Monitoring for root account logins will provide visibility into the use of a
fully privileged account and an opportunity to reduce the use of it.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ \$.userIdentity.type = "Root" && \$.userIdentity.invokedBy
NOT EXISTS && \$.eventType != "AwsServiceEvent" }"

1.  Note the \<root_usage_metric\> value associated with the filterPattern found
    in step 3.

2.  Get a list of CloudWatch alarms and filter on the \<root_usage_metric\>
    captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<root_usage_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    "Root" account usage and the \<cloudtrail_log_group_name\> taken from audit
    step 1.

aws logs put-metric-filter --log-group-name \`\<cloudtrail_log_group_name\>\`
-filter-name \`\<root_usage_metric\>\` --metric-transformations metricName=
\`\<root_usage_metric\>\` ,metricNamespace=‘MIBenchmark’,metricValue=1
--filterpattern '{ \$.userIdentity.type = "Root" && \$.userIdentity.invokedBy
NOT

EXISTS && \$.eventType != "AwsServiceEvent" }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<root_usage_alarm\>\`
--metricname \`\<root_usage_metric\>\` --statistic Sum --period 300 --threshold
1 -comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1
-namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

| correct syntax: { \$.userIdentity.type = "Root" && \$.userIdentity.invokedBy NOT EXISTS && \$.eventType != "AwsServiceEvent" } |
|--------------------------------------------------------------------------------------------------------------------------------|


**References:**

1.  CCE-79188-9

2.  CIS CSC v6.0 \#4.6, \#5.1, \#5.5

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

4.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

5.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

**Configuring log metric filter and alarm on Multi-region (global) CloudTrail**

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

4.9 *Log and Alert on Unsuccessful Administrative Account Login*

Configure systems to issue a log entry and alert on unsuccessful logins to an
administrative account.

### 3.4 Ensure a log metric filter and alarm exist for IAM policy changes (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established changes made to
Identity and Access Management (IAM) policies.

**Rationale:**

Monitoring changes to IAM policies will help ensure authentication and
authorization controls remain intact.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

1. Identify the log group name configured for use with active multi-region
CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events aws
    cloudtrail get-event-selectors --trail-name \<trailname shown in
    describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern":

"{(\$.eventName=DeleteGroupPolicy)\|\|(\$.eventName=DeleteRolePolicy)\|\|(\$.eventNa
me=DeleteUserPolicy)\|\|(\$.eventName=PutGroupPolicy)\|\|(\$.eventName=PutRolePolic
y)\|\|(\$.eventName=PutUserPolicy)\|\|(\$.eventName=CreatePolicy)\|\|(\$.eventName=Del
etePolicy)\|\|(\$.eventName=CreatePolicyVersion)\|\|(\$.eventName=DeletePolicyVersi
on)\|\|(\$.eventName=AttachRolePolicy)\|\|(\$.eventName=DetachRolePolicy)\|\|(\$.event
Name=AttachUserPolicy)\|\|(\$.eventName=DetachUserPolicy)\|\|(\$.eventName=AttachGr
oupPolicy)\|\|(\$.eventName=DetachGroupPolicy)}"

1.  Note the \<iam_changes_metric\> value associated with the filterPattern
    found in step 3.

2.  Get a list of CloudWatch alarms and filter on the \<iam_changes_metric\>
    captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<iam_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Correct syntax: for "filterPattern":

| {(\$.eventName=DeleteGroupPolicy)\|\|(\$.eventName=DeleteRolePolicy)\|\|(\$.eventName=DeleteUserPolicy)\|\|(\$.eventName=PutGroupPolicy)\|\|(\$.eventName=PutRolePolicy)\|\|(\$.eventName=PutUserPolicy)\|\|(\$.eventName=CreatePolicy)\|\|(\$.eventName=DeletePolicy)\|\|(\$.eventName=CreatePolicyVersion)\|\|(\$.eventName=DeletePolicyVersion)\|\|(\$.eventName=AttachRolePolicy)\|\|(\$.eventName=DetachRolePolicy)\|\|(\$.eventName=AttachUserPolicy)\|\|(\$.eventName=DetachUserPolicy)\|\|(\$.eventName=AttachGroupPolicy)\|\|(\$.eventName=DetachGroupPolicy)} |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|


<https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html#cloudwatch-alarms-for-cloudtrail-iam-policy-changes>

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for IAM
    policy changes and the \<cloudtrail_log_group_name\> taken from audit step
    1.

aws logs put-metric-filter --log-group-name \`\<cloudtrail_log_group_name\>\`
-filter-name \`\<iam_changes_metric\>\` --metric-transformations metricName=
\`\<iam_changes_metric\>\` ,metricNamespace=‘MIBenchmark’,metricValue=1
-filter-pattern

'{(\$.eventName=DeleteGroupPolicy)\|\|(\$.eventName=DeleteRolePolicy)\|\|(\$.eventNa
me=DeleteUserPolicy)\|\|(\$.eventName=PutGroupPolicy)\|\|(\$.eventName=PutRolePolic
y)\|\|(\$.eventName=PutUserPolicy)\|\|(\$.eventName=CreatePolicy)\|\|(\$.eventName=Del
etePolicy)\|\|(\$.eventName=CreatePolicyVersion)\|\|(\$.eventName=DeletePolicyVersi
on)\|\|(\$.eventName=AttachRolePolicy)\|\|(\$.eventName=DetachRolePolicy)\|\|(\$.event
Name=AttachUserPolicy)\|\|(\$.eventName=DetachUserPolicy)\|\|(\$.eventName=AttachGr
oupPolicy)\|\|(\$.eventName=DetachGroupPolicy)}'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<iam_changes_alarm\>\`
-metric-name \`\<iam_changes_metric\>\` --statistic Sum --period 300 --threshold
1 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1

\--namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  CCE-79189-7

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

4.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

16 *Account Monitoring and Control*

Account Monitoring and Control

### 3.5 Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for detecting
changes to CloudTrail's configurations.

**Rationale:**

Monitoring changes to CloudTrail's configuration will help ensure sustained
visibility to activities performed in the AWS account.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = CreateTrail) \|\| (\$.eventName =

UpdateTrail) \|\| (\$.eventName = DeleteTrail) \|\| (\$.eventName =
StartLogging)

\|\| (\$.eventName = StopLogging) }"

1.  Note the \<cloudtrail_cfg_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<cloudtrail_cfg_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<cloudtrail_cfg_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    cloudtrail configuration changes and the \<cloudtrail_log_group_name\> taken
    from audit step

>   1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<cloudtrail_cfg_changes_metric\>\` --metric-transformations
metricName= \`\<cloudtrail_cfg_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = CreateTrail) \|\| (\$.eventName = UpdateTrail) \|\|
(\$.eventName =

DeleteTrail) \|\| (\$.eventName = StartLogging) \|\| (\$.eventName =
StopLogging) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name
\`\<cloudtrail_cfg_changes_alarm\>\` --metric-name

\`\<cloudtrail_cfg_changes_metric\>\` --statistic Sum --period 300 --threshold 1

\--comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1
-namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  CCE-79190-5

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

4.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

6 *Maintenance, Monitoring and Analysis of Audit Logs*

Maintenance, Monitoring and Analysis of Audit Logs

### 3.6 Ensure a log metric filter and alarm exist for AWS Management 

### Console authentication failures (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for failed console
authentication attempts.

**Rationale:**

Monitoring failed console logins may decrease lead time to detect an attempt to
brute force a credential, which may provide an indicator, such as source IP,
that can be used in other event correlation.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = ConsoleLogin) && (\$.errorMessage = "Failed
authentication") }"

1.  Note the \<console_signin_failure_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<console_signin_failure_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<console_signin_failure_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for AWS
    management Console Login Failures and the \<cloudtrail_log_group_name\>
    taken from audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<console_signin_failure_metric\>\` --metric-transformations
metricName= \`\<console_signin_failure_metric\>\`
,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = ConsoleLogin) && (\$.errorMessage = "Failed authentication") }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name
\`\<console_signin_failure_alarm\>\` --metric-name

\`\<console_signin_failure_metric\>\` --statistic Sum --period 300 --threshold 1

\--comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1
-namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  CCE-79191-3

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

4.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

### 3.7 Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs (Scored) 

**Profile Applicability:**

-   Level 2

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for customer
created CMKs which have changed state to disabled or scheduled deletion.

**Rationale:**

Data encrypted with disabled or deleted keys will no longer be accessible.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{(\$.eventSource = kms.amazonaws.com) &&

((\$.eventName=DisableKey)\|\|(\$.eventName=ScheduleKeyDeletion)) }"

1.  Note the \<disable_or_delete_cmk_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<disable_or_delete_cmk_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<disable_or_delete_cmk_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    disabled or scheduled for deletion CMK's and the
    \<cloudtrail_log_group_name\> taken from audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<disable_or_delete_cmk_changes_metric\>\`
--metrictransformations metricName= \`\<disable_or_delete_cmk_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{(\$.eventSource
= kms.amazonaws.com) &&

((\$.eventName=DisableKey)\|\|(\$.eventName=ScheduleKeyDeletion)) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name

\`\<disable_or_delete_cmk_changes_alarm\>\` --metric-name

\`\<disable_or_delete_cmk_changes_metric\>\` --statistic Sum --period 300
-threshold 1 --comparison-operator GreaterThanOrEqualToThreshold
--evaluationperiods 1 --namespace ‘MIBenchmark’ --alarm-actions
\<sns_topic_arn\>

**References:**

1.  CCE-79192-1

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

4.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

#### 3.8 Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for changes to S3
bucket policies.

**Rationale:**

Monitoring changes to S3 bucket policies may reduce time to detect and correct
permissive policies on sensitive S3 buckets.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventSource = s3.amazonaws.com) && ((\$.eventName =

PutBucketAcl) \|\| (\$.eventName = PutBucketPolicy) \|\| (\$.eventName =

PutBucketCors) \|\| (\$.eventName = PutBucketLifecycle) \|\| (\$.eventName =

PutBucketReplication) \|\| (\$.eventName = DeleteBucketPolicy) \|\|
(\$.eventName =

DeleteBucketCors) \|\| (\$.eventName = DeleteBucketLifecycle) \|\| (\$.eventName
= DeleteBucketReplication)) }"

1.  Note the \<s3_bucket_policy_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<s3_bucket_policy_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<s3_bucket_policy_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

>   1. Create a metric filter based on filter pattern provided which checks for
>   S3 bucket policy changes and the \<cloudtrail_log_group_name\> taken from
>   audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<s3_bucket_policy_changes_metric\>\` --metric-transformations
metricName= \`\<s3_bucket_policy_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventSource = s3.amazonaws.com) && ((\$.eventName = PutBucketAcl) \|\|

(\$.eventName = PutBucketPolicy) \|\| (\$.eventName = PutBucketCors) \|\|

(\$.eventName = PutBucketLifecycle) \|\| (\$.eventName = PutBucketReplication)
\|\| (\$.eventName = DeleteBucketPolicy) \|\| (\$.eventName = DeleteBucketCors)
\|\|

(\$.eventName = DeleteBucketLifecycle) \|\| (\$.eventName =

DeleteBucketReplication)) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name
\`\<s3_bucket_policy_changes_alarm\>\` --metric-name

\`\<s3_bucket_policy_changes_metric\>\` --statistic Sum --period 300 --threshold

1 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1

\--namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

#### 3.9 Ensure a log metric filter and alarm exist for AWS Config configuration changes (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms. It
is recommended that a metric filter and alarm be established for detecting
changes to CloudTrail's configurations.

**Rationale:**

Monitoring changes to AWS Config configuration will help ensure sustained
visibility of configuration items within the AWS account.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventSource = config.amazonaws.com) &&

((\$.eventName=StopConfigurationRecorder)\|\|(\$.eventName=DeleteDeliveryChannel)
\|\|(\$.eventName=PutDeliveryChannel)\|\|(\$.eventName=PutConfigurationRecorder))
}"

1.  Note the \<aws_config_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the
    \<aws_config_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<aws_config_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for AWS
    Configuration changes and the \<cloudtrail_log_group_name\> taken from audit
    step 1.

| aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\> -filter-name \`\<aws_config_changes_metric\>\` --metric-transformations metricName= \`\<aws_config_changes_metric\>\` ,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{ (\$.eventSource = config.amazonaws.com) && ((\$.eventName=StopConfigurationRecorder)\|\|(\$.eventName=DeleteDeliveryChannel) \|\|(\$.eventName=PutDeliveryChannel)\|\|(\$.eventName=PutConfigurationRecorder)) }' |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|


**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<aws_config_changes_alarm\>\`
-metric-name \`\<aws_config_changes_metric\>\` --statistic Sum --period 300
-threshold 1 --comparison-operator GreaterThanOrEqualToThreshold
--evaluationperiods 1 --namespace ‘MIBenchmark’ --alarm-actions
\<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

1.4 *Maintain Detailed Asset Inventory*

Maintain an accurate and up-to-date inventory of all technology assets with the
potential to store or process information. This inventory shall include all
hardware assets, whether connected to the organization's network or not.

11.2 *Document Traffic Configuration Rules*

All configuration rules that allow traffic to flow through network devices
should be documented in a configuration management system with a specific
business reason for each rule, a specific individual’s name responsible for that
business need, and an expected duration of the need.

16.1 *Maintain an Inventory of Authentication Systems*

Maintain an inventory of each of the organization's authentication systems,
including those located onsite or at a remote service provider.

#### 3.10 Ensure a log metric filter and alarm exist for security group changes (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to

CloudWatch Logs and establishing corresponding metric filters and alarms.
Security Groups are a stateful packet filter that controls ingress and egress
traffic within a VPC. It is recommended that a metric filter and alarm be
established changes to Security Groups.

**Rationale:**

Monitoring changes to security group will help ensure that resources and
services are not unintentionally exposed.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = AuthorizeSecurityGroupIngress) \|\|

(\$.eventName = AuthorizeSecurityGroupEgress) \|\| (\$.eventName =

RevokeSecurityGroupIngress) \|\| (\$.eventName = RevokeSecurityGroupEgress) \|\|

(\$.eventName = CreateSecurityGroup) \|\| (\$.eventName = DeleteSecurityGroup)
}"

1.  Note the \<security_group_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the

>   \<security_group_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<security_group_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    security groups changes and the \<cloudtrail_log_group_name\> taken from
    audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<security_group_changes_metric\>\` --metric-transformations
metricName= \`\<security_group_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = AuthorizeSecurityGroupIngress) \|\| (\$.eventName =

AuthorizeSecurityGroupEgress) \|\| (\$.eventName = RevokeSecurityGroupIngress)

\|\| (\$.eventName = RevokeSecurityGroupEgress) \|\| (\$.eventName =
CreateSecurityGroup) \|\| (\$.eventName = DeleteSecurityGroup) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name
\`\<security_group_changes_alarm\>\` --metric-name

\`\<security_group_changes_metric\>\` --statistic Sum --period 300 --threshold 1

\--comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1
-namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

4.8 *Log and Alert on Changes to Administrative Group Membership*

Configure systems to issue a log entry and alert when an account is added to or
removed from any group assigned administrative privileges.

#### 3.11 Ensure a log metric filter and alarm exist for changes to Network 

#### Access Control Lists (NACL) (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to

CloudWatch Logs and establishing corresponding metric filters and alarms. NACLs
are used as a stateless packet filter to control ingress and egress traffic for
subnets within a VPC. It is recommended that a metric filter and alarm be
established for changes made to NACLs.

**Rationale:**

Monitoring changes to NACLs will help ensure that AWS resources and services are
not unintentionally exposed.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = CreateNetworkAcl) \|\| (\$.eventName =

CreateNetworkAclEntry) \|\| (\$.eventName = DeleteNetworkAcl) \|\| (\$.eventName
=

DeleteNetworkAclEntry) \|\| (\$.eventName = ReplaceNetworkAclEntry) \|\|

(\$.eventName = ReplaceNetworkAclAssociation) }"

1.  Note the \<nacl_changes_metric\> value associated with the filterPattern
    found in step 3.

2.  Get a list of CloudWatch alarms and filter on the \<nacl_changes_metric\>
    captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<nacl_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    NACL changes and the \<cloudtrail_log_group_name\> taken from audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<nacl_changes_metric\>\` --metric-transformations metricName=
\`\<nacl_changes_metric\>\` ,metricNamespace=‘MIBenchmark’,metricValue=1
-filter-pattern '{ (\$.eventName = CreateNetworkAcl) \|\| (\$.eventName =
CreateNetworkAclEntry) \|\| (\$.eventName = DeleteNetworkAcl) \|\| (\$.eventName
=

DeleteNetworkAclEntry) \|\| (\$.eventName = ReplaceNetworkAclEntry) \|\|

(\$.eventName = ReplaceNetworkAclAssociation) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<nacl_changes_alarm\>\`
-metric-name \`\<nacl_changes_metric\>\` --statistic Sum --period 300 -threshold
1 --comparison-operator GreaterThanOrEqualToThreshold --evaluationperiods 1
--namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

11.3 *Use Automated Tools to Verify Standard Device Configurations and Detect
Changes* Compare all network device configuration against approved security
configurations defined for each network device in use and alert when any
deviations are discovered.

#### 3.12 Ensure a log metric filter and alarm exist for changes to network 

#### gateways (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms.
Network gateways are required to send/receive traffic to a destination outside
of a VPC. It is recommended that a metric filter and alarm be established for
changes to network gateways.

**Rationale:**

Monitoring changes to network gateways will help ensure that all ingress/egress
traffic traverses the VPC border via a controlled path.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = CreateCustomerGateway) \|\| (\$.eventName =

DeleteCustomerGateway) \|\| (\$.eventName = AttachInternetGateway) \|\|
(\$.eventName = CreateInternetGateway) \|\| (\$.eventName =

DeleteInternetGateway) \|\| (\$.eventName = DetachInternetGateway) }"

1.  Note the \<network_gw_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the
    \<network_gw_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<network_gw_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    network gateways changes and the \<cloudtrail_log_group_name\> taken from
    audit step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<network_gw_changes_metric\>\` --metric-transformations
metricName= \`\<network_gw_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = CreateCustomerGateway) \|\| (\$.eventName =

DeleteCustomerGateway) \|\| (\$.eventName = AttachInternetGateway) \|\|
(\$.eventName = CreateInternetGateway) \|\| (\$.eventName =

DeleteInternetGateway) \|\| (\$.eventName = DetachInternetGateway) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<network_gw_changes_alarm\>\`
-metric-name \`\<network_gw_changes_metric\>\` --statistic Sum --period 300
-threshold 1 --comparison-operator GreaterThanOrEqualToThreshold
--evaluationperiods 1 --namespace ‘MIBenchmark’ --alarm-actions
\<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

11.3 *Use Automated Tools to Verify Standard Device Configurations and Detect
Changes* Compare all network device configuration against approved security
configurations defined for each network device in use and alert when any
deviations are discovered.

#### 3.13 Ensure a log metric filter and alarm exist for route table changes (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to CloudWatch Logs and establishing corresponding metric filters and alarms.
Routing tables are used to route network traffic between subnets and to network
gateways. It is recommended that a metric filter and alarm be established for
changes to route tables.

**Rationale:**

Monitoring changes to route tables will help ensure that all VPC traffic flows
through an expected path.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

>   1. Identify the log group name configured for use with active multi-region
>   CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,
\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events

aws cloudtrail get-event-selectors --trail-name \<trailname shown in
describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = CreateRoute) \|\| (\$.eventName =

CreateRouteTable) \|\| (\$.eventName = ReplaceRoute) \|\| (\$.eventName =

ReplaceRouteTableAssociation) \|\| (\$.eventName = DeleteRouteTable) \|\|
(\$.eventName = DeleteRoute) \|\| (\$.eventName = DisassociateRouteTable) }"

1.  Note the \<route_table_changes_metric\> value associated with the
    filterPattern found in step 3.

2.  Get a list of CloudWatch alarms and filter on the
    \<route_table_changes_metric\> captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<route_table_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for
    route table changes and the \<cloudtrail_log_group_name\> taken from audit
    step 1.

aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\>
-filter-name \`\<route_table_changes_metric\>\` --metric-transformations
metricName= \`\<route_table_changes_metric\>\`

,metricNamespace=‘MIBenchmark’,metricValue=1 --filter-pattern '{

(\$.eventName = CreateRoute) \|\| (\$.eventName = CreateRouteTable) \|\|

(\$.eventName = ReplaceRoute) \|\| (\$.eventName = ReplaceRouteTableAssociation)

\|\| (\$.eventName = DeleteRouteTable) \|\| (\$.eventName = DeleteRoute) \|\|

(\$.eventName = DisassociateRouteTable) }'

**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<route_table_changes_alarm\>\`
--metric-name \`\<route_table_changes_metric\>\` --statistic Sum --period 300
-threshold 1 --comparison-operator GreaterThanOrEqualToThreshold
-evaluation-periods 1 --namespace ‘MIBenchmark’ --alarm-actions

\<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

6.2 *Activate audit logging*

Ensure that local logging has been enabled on all systems and networking
devices.

11.3 *Use Automated Tools to Verify Standard Device Configurations and Detect
Changes* Compare all network device configuration against approved security
configurations defined for each network device in use and alert when any
deviations are discovered.

#### 3.14 Ensure a log metric filter and alarm exist for VPC changes (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Real-time monitoring of API calls can be achieved by directing CloudTrail Logs
to

CloudWatch Logs and establishing corresponding metric filters and alarms. It is
possible to have more than 1 VPC within an account, in addition it is also
possible to create a peer connection between 2 VPCs enabling network traffic to
route between VPCs. It is recommended that a metric filter and alarm be
established for changes made to VPCs.

**Rationale:**

Monitoring changes to IAM policies will help ensure authentication and
authorization controls remain intact.

**Audit:**

Perform the following to ensure that there is at least one active multi-region
CloudTrail with prescribed metric filters and alarms configured:

1. Identify the log group name configured for use with active multi-region
CloudTrail:

-   List all CloudTrails: aws cloudtrail describe-trails

-   Identify Multi region Cloudtrails: Trails with "IsMultiRegionTrail" set to
    true

-   From value associated with CloudWatchLogsLogGroupArn note

>   \<cloudtrail_log_group_name\>

Example: for CloudWatchLogsLogGroupArn that looks like

arn:aws:logs:\<region\>:\<aws_account_number\>:log-group:NewGroup:\*,

\<cloudtrail_log_group_name\> would be NewGroup

-   Ensure Identified Multi region CloudTrail is active aws cloudtrail
    get-trail-status --name \<Name of a Multi-region CloudTrail\> ensure
    IsLogging is set to TRUE

-   Ensure identified Multi-region Cloudtrail captures all Management Events aws
    cloudtrail get-event-selectors --trail-name \<trailname shown in
    describetrails\>

Ensure there is at least one Event Selector for a Trail with
IncludeManagementEvents set to true and ReadWriteType set to All

1.  Get a list of all associated metric filters for this
    \<cloudtrail_log_group_name\>:

aws logs describe-metric-filters --log-group-name
"\<cloudtrail_log_group_name\>"

1.  Ensure the output from the above command contains the following:

"filterPattern": "{ (\$.eventName = CreateVpc) \|\| (\$.eventName = DeleteVpc)
\|\|

(\$.eventName = ModifyVpcAttribute) \|\| (\$.eventName =

AcceptVpcPeeringConnection) \|\| (\$.eventName = CreateVpcPeeringConnection)
\|\|

(\$.eventName = DeleteVpcPeeringConnection) \|\| (\$.eventName =

RejectVpcPeeringConnection) \|\| (\$.eventName = AttachClassicLinkVpc) \|\|

(\$.eventName = DetachClassicLinkVpc) \|\| (\$.eventName =
DisableVpcClassicLink)

\|\| (\$.eventName = EnableVpcClassicLink) }"

1.  Note the \<vpc_changes_metric\> value associated with the filterPattern
    found in step 3.

2.  Get a list of CloudWatch alarms and filter on the \<vpc_changes_metric\>
    captured in step 4.

aws cloudwatch describe-alarms --query 'MetricAlarms[?MetricName==
\`\<vpc_changes_metric\>\`]'

1.  Note the AlarmActions value - this will provide the SNS topic ARN value. 7.
    Ensure there is at least one active subscriber to the SNS topic

aws sns list-subscriptions-by-topic --topic-arn \<sns_topic_arn\>

at least one subscription should have "SubscriptionArn" with valid aws ARN.

Example of valid "SubscriptionArn":

"arn:aws:sns:\<region\>:\<aws_account_number\>:\<SnsTopicName\>:\<SubscriptionID\>"

**Remediation:**

Perform the following to setup the metric filter, alarm, SNS topic, and
subscription:

1.  Create a metric filter based on filter pattern provided which checks for VPC
    changes and the \<cloudtrail_log_group_name\> taken from audit step 1.

| aws logs put-metric-filter --log-group-name \<cloudtrail_log_group_name\> -filter-name \`\<vpc_changes_metric\>\` --metric-transformations metricName= \`\<vpc_changes_metric\>\` ,metricNamespace=‘MIBenchmark’,metricValue=1 -filter-pattern '{ (\$.eventName = CreateVpc) \|\| (\$.eventName = DeleteVpc) \|\| (\$.eventName = ModifyVpcAttribute) \|\| (\$.eventName = AcceptVpcPeeringConnection) \|\| (\$.eventName = CreateVpcPeeringConnection) \|\| (\$.eventName = DeleteVpcPeeringConnection) \|\| (\$.eventName = RejectVpcPeeringConnection) \|\| (\$.eventName = AttachClassicLinkVpc) \|\| (\$.eventName = DetachClassicLinkVpc) \|\| (\$.eventName = DisableVpcClassicLink) \|\| (\$.eventName = EnableVpcClassicLink) }' |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|


**Note**: You can choose your own metricName and metricNamespace strings. Using
the same metricNamespace for all Foundations Benchmark metrics will group them
together.

1.  Create an SNS topic that the alarm will notify

aws sns create-topic --name \<sns_topic_name\>

**Note**: you can execute this command once and then re-use the same topic for
all monitoring alarms.

1.  Create an SNS subscription to the topic created in step 2

aws sns subscribe --topic-arn \<sns_topic_arn\> --protocol \<protocol_for_sns\>
-notification-endpoint \<sns_subscription_endpoints\>

**Note**: you can execute this command once and then re-use the SNS subscription
for all monitoring alarms.

1.  Create an alarm that is associated with the CloudWatch Logs Metric Filter
    created in step 1 and an SNS topic created in step 2

aws cloudwatch put-metric-alarm --alarm-name \`\<vpc_changes_alarm\>\`
-metric-name \`\<vpc_changes_metric\>\` --statistic Sum --period 300 --threshold
1 --comparison-operator GreaterThanOrEqualToThreshold --evaluation-periods 1

\--namespace ‘MIBenchmark’ --alarm-actions \<sns_topic_arn\>

**References:**

1.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtraillog-files-from-multiple-regions.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/receive-cloudtrail-log-files-from-multiple-regions.html)

2.  [https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarmsfor-cloudtrail.html
    ](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/cloudwatch-alarms-for-cloudtrail.html)

3.  [https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html
    ](https://docs.aws.amazon.com/sns/latest/dg/SubscribeTopic.html)

**Notes:**

Configuring log metric filter and alarm on Multi-region (global) CloudTrail

-   ensures that activities from all regions (used as well as unused) are
    monitored

-   ensures that activities on all supported global services are monitored

-   ensures that all management events across all regions are monitored

**CIS Controls:**

5.5 *Implement Automated Configuration Monitoring Systems*

Utilize a Security Content Automation Protocol (SCAP) compliant configuration
monitoring system to verify all security configuration elements, catalog
approved exceptions, and alert when unauthorized changes occur.

*4 Networking* 
---------------

This section contains recommendations for configuring security-related aspects
of the default Virtual Private Cloud (VPC)

#### 4.1 Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Security groups provide stateful filtering of ingress/egress network traffic to
AWS resources. It is recommended that no security group allows unrestricted
ingress access to port 22 .

**Rationale:**

Removing unfettered connectivity to remote console services, such as SSH,
reduces a server's exposure to risk.

**Audit:**

Perform the following to determine if the account is configured as prescribed:

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  In the left pane, click Security Groups

3.  For each security group, perform the following:

4.  Select the security group

5.  Click the Inbound Rules tab

6.  Ensure no rule exists that has a port range that includes port 22 and has a
    Source of

>   0.0.0.0/0

Note: A Port value of ALL or a port range such as 0-1024 are inclusive of port
22 .

**Remediation:**

Perform the following to implement the prescribed state:

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  In the left pane, click Security Groups

3.  For each security group, perform the following:

4.  Select the security group

5.  Click the Inbound Rules tab

6.  Identify the rules to be removed

7.  Click the x in the Remove column

8.  Click Save

**Impact:**

For updating an existing environment, care should be taken to ensure that
administrators currently relying on an existing ingress from 0.0.0.0/0 have
access to ports 22 and/or 3389 through another security group.

**CIS Controls:**

9.2 *Ensure Only Approved Ports, Protocols and Services Are Running*

Ensure that only network ports, protocols, and services listening on a system
with validated business needs, are running on each system.

#### 4.2 Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 (Scored) 

**Profile Applicability:**

 Level 1

**Description:**

Security groups provide stateful filtering of ingress/egress network traffic to
AWS resources. It is recommended that no security group allows unrestricted
ingress access to port 3389 .

**Rationale:**

Removing unfettered connectivity to remote console services, such as RDP,
reduces a server's exposure to risk.

**Audit:**

Perform the following to determine if the account is configured as prescribed:

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  In the left pane, click Security Groups

3.  For each security group, perform the following:

4.  Select the security group

5.  Click the Inbound Rules tab

6.  Ensure no rule exists that has a port range that includes port 3389 and has
    a Source of 0.0.0.0/0

Note: A Port value of ALL or a port range such as 1024-4098 are inclusive of
port 3389 .

**Remediation:**

Perform the following to implement the prescribed state:

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  In the left pane, click Security Groups

3.  For each security group, perform the following:

4.  Select the security group

5.  Click the Inbound Rules tab

6.  Identify the rules to be removed

7.  Click the x in the Remove column

8.  Click Save

**Impact:**

For updating an existing environment, care should be taken to ensure that
administrators currently relying on an existing ingress from 0.0.0.0/0 have
access to ports 22 and/or 3389 through another security group.

**CIS Controls:**

9.2 *Ensure Only Approved Ports, Protocols and Services Are Running*

Ensure that only network ports, protocols, and services listening on a system
with validated business needs, are running on each system.

#### 4.3 Ensure the default security group of every VPC restricts all traffic (Scored) 

**Profile Applicability:**

 Level 2

**Description:**

A VPC comes with a default security group whose initial settings deny all
inbound traffic, allow all outbound traffic, and allow all traffic between
instances assigned to the security group. If you don't specify a security group
when you launch an instance, the instance is automatically assigned to this
default security group. Security groups provide stateful filtering of
ingress/egress network traffic to AWS resources. It is recommended that the
default security group restrict all traffic.

The default VPC in every region should have its default security group updated
to comply. Any newly created VPCs will automatically contain a default security
group that will need remediation to comply with this recommendation.

**NOTE:** When implementing this recommendation, VPC flow logging is invaluable
in determining the least privilege port access required by systems to work
properly because it can log all packet acceptances and rejections occurring
under the current security groups. This dramatically reduces the primary barrier
to least privilege engineering - discovering the minimum ports required by
systems in the environment. Even if the VPC flow logging recommendation in this
benchmark is not adopted as a permanent security measure, it should be used
during any period of discovery and engineering for least privileged security
groups.

**Rationale:**

Configuring all VPC default security groups to restrict all traffic will
encourage least privilege security group development and mindful placement of
AWS resources into security groups which will in-turn reduce the exposure of
those resources.

**Audit:**

Perform the following to determine if the account is configured as prescribed:

Security Group State

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  Repeat the next steps for all VPCs - including the default VPC in each AWS
    region:

3.  In the left pane, click Security Groups

4.  For each default security group, perform the following:

5.  Select the default security group

6.  Click the Inbound Rules tab

7.  Ensure no rule exist

8.  Click the Outbound Rules tab

9.  Ensure no rules exist

Security Group Members

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  Repeat the next steps for all default groups in all VPCs - including the
    default VPC in each AWS region:

3.  In the left pane, click Security Groups 4. Copy the id of the default
    security group.

4.  Change to the EC2 Management Console at
    https://console.aws.amazon.com/ec2/v2/home

5.  In the filter column type 'Security Group ID : \< security group id from \#4
    \>'

**Remediation:**

Security Group Members

Perform the following to implement the prescribed state:

1.  Identify AWS resources that exist within the default security group

2.  Create a set of least privilege security groups for those resources

3.  Place the resources in those security groups

4.  Remove the resources noted in \#1 from the default security group

Security Group State

1.  Login to the AWS Management Console at
    [https://console.aws.amazon.com/vpc/home
    ](https://console.aws.amazon.com/vpc/home)

2.  Repeat the next steps for all VPCs - including the default VPC in each AWS
    region:

3.  In the left pane, click Security Groups

4.  For each default security group, perform the following:

5.  Select the default security group

6.  Click the Inbound Rules tab

7.  Remove any inbound rules

8.  Click the Outbound Rules tab

9.  Remove any inbound rules

Recommended:

IAM groups allow you to edit the "name" field. After remediating default groups
rules for all VPCs in all regions, edit this field to add text similar to "DO
NOT USE. DO NOT ADD RULES"

**Impact:**

Implementing this recommendation in an existing VPC containing operating
resources requires extremely careful migration planning as the default security
groups are likely to be enabling many ports that are unknown. Enabling VPC flow
logging (of accepts) in an existing environment that is known to be breach free
will reveal the current pattern of ports being used for each instance to
communicate successfully.

**References:**

1.  [http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-networksecurity.html
    ](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-network-security.html)

**CIS Controls:**

14.6 *Protect Information through Access Control Lists*

Protect all information stored on systems with file system, network share,
claims, application, or database specific access control lists. These controls
will enforce the principle that only authorized individuals should have access
to the information based on their need to access the information as a part of
their responsibilities.

#### 4.4 Ensure routing tables for VPC peering are "least access" (Not Scored) 

**Profile Applicability:**

 Level 2

**Description:**

Once a VPC peering connection is established, routing tables must be updated to
establish any connections between the peered VPCs. These routes can be as
specific as desired - even peering a VPC to only a single host on the other side
of the connection.

**Rationale:**

Being highly selective in peering routing tables is a very effective way of
minimizing the impact of breach as resources outside of these routes are
inaccessible to the peered VPC.

**Audit:**

Review routing tables of peered VPCs for whether they route all subnets of each
VPC and whether that is necessary to accomplish the intended purposes for
peering the VPCs. Via CLI:

>   1. List all the route tables from a VPC and check if "GatewayId" is pointing
>   to a *\<peering_connection_id\>* (e.g. pcx-1a2b3c4d) and if
>   "DestinationCidrBlock" is as specific as desired.

aws ec2 describe-route-tables --filter "Name=vpc-id,Values=\<vpc_id\>" --query

"RouteTables[\*].{RouteTableId:RouteTableId, VpcId:VpcId, Routes:Routes,

AssociatedSubnets:Associations[\*].SubnetId}"

**Remediation:**

Remove and add route table entries to ensure that the least number of subnets or
hosts as is required to accomplish the purpose for peering are routable. Via
CLI:

1.  For each *\<route_table_id\>* containing routes non compliant with your
    routing policy (which grants more than desired "least access"), delete the
    non compliant route:

aws ec2 delete-route --route-table-id \<route_table_id\> --destination-cidrblock
\<non_compliant_destination_CIDR\>

1.  Create a new compliant route:

aws ec2 create-route --route-table-id \<route_table_id\> --destination-cidrblock
\<compliant_destination_CIDR\> --vpc-peering-connection-id

\<peering_connection_id\>

**References:**

>   [1.
>   http://docs.aws.amazon.com/AmazonVPC/latest/PeeringGuide/peeringconfigurations-partial-access.html
>   ](http://docs.aws.amazon.com/AmazonVPC/latest/PeeringGuide/peering-configurations-partial-access.html)

**CIS Controls:**

14.6 *Protect Information through Access Control Lists*

Protect all information stored on systems with file system, network share,
claims, application, or database specific access control lists. These controls
will enforce the principle that only authorized individuals should have access
to the information based on their need to access the information as a part of
their responsibilities.

Appendix: Summary Table 
========================

| **Control**  | **Set Correctly**                                                                                                |    |     |   |
|--------------|------------------------------------------------------------------------------------------------------------------|----|-----|---|
|              | Yes                                                                                                              | No | N/A |   |
| **1**        | **Identity and Access Management**                                                                               |    |     |   |
| 1.1          | Avoid the use of the "root" account (Scored)                                                                     |   |    |   |
| 1.2          | Ensure multi-factor authentication (MFA) is enabled for all IAM users that have a console password (Scored)      |   |    |   |
| 1.3          | Ensure credentials unused for 90 days or greater are disabled (Scored)                                           |   |    |   |
| 1.4          | Ensure access keys are rotated every 90 days or less (Scored)                                                    |   |    |   |
| 1.5          | Ensure IAM password policy requires at least one uppercase letter (Scored)                                       |   |    |   |
| 1.6          | Ensure IAM password policy require at least one lowercase letter (Scored)                                        |   |    |   |
| 1.7          | Ensure IAM password policy require at least one symbol (Scored)                                                  |   |    |   |
| 1.8          | Ensure IAM password policy require at least one number (Scored)                                                  |   |    |   |
| 1.9          | Ensure IAM password policy requires minimum length of 14 or greater (Scored)                                     |   |    |   |
| 1.10         | Ensure IAM password policy prevents password reuse (Scored)                                                      |   |    |   |
| 1.11         | Ensure IAM password policy expires passwords within 90 days or less (Scored)                                     |   |    |   |
| 1.12         | Ensure no root account access key exists (Scored)                                                                |   |    |   |
| 1.13         | Ensure MFA is enabled for the "root" account (Scored)                                                            |   |    |   |
| 1.14         | Ensure hardware MFA is enabled for the "root" account (Scored)                                                   |   |    |   |
| 1.15         | Ensure security questions are registered in the AWS account (Not Scored)                                         |   |    |   |
| 1.16         | Ensure IAM policies are attached only to groups or roles (Scored)                                                |   |    |   |
| 1.17         | Maintain current contact details (Not Scored)                                                                    |   |    |   |
| 1.18         | Ensure security contact information is registered (Not Scored)                                                   |   |    |   |
| 1.19         | Ensure IAM instance roles are used for AWS resource access from instances (Not Scored)                           |   |    |   |
| 1.20         | Ensure a support role has been created to manage incidents with AWS Support (Scored)                             |   |    |   |
| 1.21         | Do not setup access keys during initial user setup for all IAM users that have a console password (Not Scored)   |   |    |   |
| 1.22         | Ensure IAM policies that allow full "\*:\*" administrative privileges are not created (Scored)                   |   |    |   |
| **2**        | **Logging**                                                                                                      |    |     |   |
| 2.1          | Ensure CloudTrail is enabled in all regions (Scored)                                                             |   |    |   |
| 2.2          | Ensure CloudTrail log file validation is enabled (Scored)                                                        |   |    |   |
| 2.3          | Ensure the S3 bucket used to store CloudTrail logs is not publicly accessible (Scored)                           |   |    |   |
| 2.4          | Ensure CloudTrail trails are integrated with CloudWatch Logs (Scored)                                            |   |    |   |
| 2.5          | Ensure AWS Config is enabled in all regions (Scored)                                                             |   |    |   |
| 2.6          | Ensure S3 bucket access logging is enabled on the CloudTrail S3 bucket (Scored)                                  |   |    |   |
| 2.7          | Ensure CloudTrail logs are encrypted at rest using KMS CMKs (Scored)                                             |   |    |   |
| 2.8          | Ensure rotation for customer created CMKs is enabled (Scored)                                                    |   |    |   |
| 2.9          | Ensure VPC flow logging is enabled in all VPCs (Scored)                                                          |   |    |   |
| **3**        | **Monitoring**                                                                                                   |    |     |   |
| 3.1          | Ensure a log metric filter and alarm exist for unauthorized API calls (Scored)                                   |   |    |   |
| 3.2          | Ensure a log metric filter and alarm exist for Management Console sign-in without MFA (Scored)                   |   |    |   |
| 3.3          | Ensure a log metric filter and alarm exist for usage of "root" account (Scored)                                  |   |    |   |
| 3.4          | Ensure a log metric filter and alarm exist for IAM policy changes (Scored)                                       |   |    |   |
| 3.5          | Ensure a log metric filter and alarm exist for CloudTrail configuration changes (Scored)                         |   |    |   |
| 3.6          | Ensure a log metric filter and alarm exist for AWS Management Console authentication failures (Scored)           |   |    |   |
| 3.7          | Ensure a log metric filter and alarm exist for disabling or scheduled deletion of customer created CMKs (Scored) |   |    |   |
| 3.8          | Ensure a log metric filter and alarm exist for S3 bucket policy changes (Scored)                                 |   |    |   |
| 3.9          | Ensure a log metric filter and alarm exist for AWS Config configuration changes (Scored)                         |   |    |   |
| 3.10         | Ensure a log metric filter and alarm exist for security group changes (Scored)                                   |   |    |   |
| 3.11         | Ensure a log metric filter and alarm exist for changes to Network Access Control Lists (NACL) (Scored)           |   |    |   |
| 3.12         | Ensure a log metric filter and alarm exist for changes to network gateways (Scored)                              |   |    |   |
| 3.13         | Ensure a log metric filter and alarm exist for route table changes (Scored)                                      |   |    |   |
| 3.14         | Ensure a log metric filter and alarm exist for VPC changes (Scored)                                              |   |    |   |
| **4**        | **Networking**                                                                                                   |    |     |   |
| 4.1          | Ensure no security groups allow ingress from 0.0.0.0/0 to port 22 (Scored)                                       |   |    |   |
| 4.2          | Ensure no security groups allow ingress from 0.0.0.0/0 to port 3389 (Scored)                                     |   |    |   |
| 4.3          | Ensure the default security group of every VPC restricts all traffic (Scored)                                    |   |    |   |
| 4.4          | Ensure routing tables for VPC peering are "least access" (Not Scored)                                            |   |    |   |
