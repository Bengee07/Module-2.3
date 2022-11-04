## Brief

### Preparation

To access AWS services with the AWS CLI, you need an AWS account, IAM credentials, and an IAM access key pair. When running AWS CLI commands, the AWS CLI needs to have access to those AWS credentials.

- Install Visual Studio Code
- Install NPM
- Install AWS CLI

### Lesson Overview


The AWS Command Line Interface (AWS CLI) is an open source tool that enables you to interact with AWS services using commands in your command-line shell. With minimal configuration, the AWS CLI enables you to start running commands that implement functionality equivalent to that provided by the browser-based AWS Management Console from the command prompt in your terminal program:


- **Linux shells** – Use common shell programs such as bash, zsh, and tcsh to run commands in Linux or macOS.
- **Windows command line** – On Windows, run commands at the Windows command prompt or in PowerShell.
- **Remotely** – Run commands on Amazon Elastic Compute Cloud (Amazon EC2) instances through a remote terminal program such as PuTTY or SSH, or with AWS Systems Manager.


All IaaS (infrastructure as a service) AWS administration, management, and access functions in the AWS Management Console are available in the AWS API and AWS CLI. New AWS IaaS features and services provide full AWS Management Console functionality through the API and CLI at launch or within 180 days of launch.

The AWS CLI provides direct access to the public APIs of AWS services. You can explore a service's capabilities with the AWS CLI, and develop shell scripts to manage your resources. In addition to the low-level, API-equivalent commands, several AWS services provide customizations for the AWS CLI. Customizations can include higher-level commands that simplify using a service with a complex API.


---

## Part 1 - Prerequisites to use the AWS CLI

Step 1: Sign up to AWS

Step 2: Create an IAM user account

Step 3: Create an access key ID and secret access key

Step 4: Install AWS CLI using this link: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

---

## Part 2 - Setup AWS CLI Configuration

### Quick configuration with `aws configure`

The AWS CLI stores this information in a profile (a collection of settings) named `default` in the `credentials` file. By default, the information in this profile is used when you run an AWS CLI command that doesn't explicitly specify a profile to use. For more information on the credentials file, see Configuration and credential file settings

The following example shows sample values. Replace them with your own values as described in the following sections.

```
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
```

### Access key ID and Secret Access Key

Access keys use an access key ID and secret access key that you use to sign programmatic requests to AWS.


Access keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS. If you don't have access keys, you can create them from the AWS Management Console. As a best practice, do not use the AWS account root user access keys for any task where it's not required. Instead, create a new administrator IAM user with access keys for yourself.


The only time that you can view or download the secret access key is when you create the keys. You cannot recover them later. However, you can create new access keys at any time. You must also have permissions to perform the required IAM actions. For more information, see Permissions required to access IAM resources in the IAM User Guide.


To create access keys for an IAM user

1. Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.
2. In the navigation pane, choose Users.
3. Choose the name of the user whose access keys you want to create, and then choose the Security credentials tab.
4. In the Access keys section, choose Create access key.
5. To view the new access key pair, choose Show. You will not have access to the secret access key again after this dialog box closes. Your credentials will look something like this:

        - Access key ID: AKIAIOSFODNN7EXAMPLE
        - Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

<img width="1680" alt="image" src="https://user-images.githubusercontent.com/106639884/187820309-015034cd-cbc6-4c4d-9871-aee939d79cf6.png">

6. To download the key pair, choose Download .csv file. Store the keys in a secure location. You will not have access to the secret access key again after this dialog box closes. Keep the keys confidential in order to protect your AWS account and never email them. Do not share them outside your organization, even if an inquiry appears to come from AWS or Amazon.com. No one who legitimately represents Amazon will ever ask you for your secret key.
7. After you download the .csv file, choose Close. When you create an access key, the key pair is active by default, and you can use the pair right away.



---

## Part 3 - Amazon S3 with CLI

You can view the contents of your S3 buckets in a directory-based listing by using a familiar syntax.

```
$ aws s3 ls s3://mybucket
        LastWriteTime            Length Name
        ------------             ------ ----
                                PRE myfolder/
2022-09-01 09:00:00           1234 myfile.txt
```

You can perform recursive uploads and downloads of multiple files in a single folder-level command. The AWS CLI will run these transfers in parallel for increased performance.

```
$ aws s3 cp myfolder s3://mybucket/myfolder --recursive
upload: myfolder/file1.txt to s3://mybucket/myfolder/file1.txt
upload: myfolder/subfolder/file1.txt to s3://mybucket/myfolder/subfolder/file1.txt
```

A sync command makes it easy to synchronize the contents of a local folder with a copy in an S3 bucket.

```
$ aws s3 sync myfolder s3://mybucket/myfolder --exclude *.tmp
upload: myfolder/newfile.txt to s3://mybucket/myfolder/newfile.txt
```
