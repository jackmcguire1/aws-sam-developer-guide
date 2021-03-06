# Installing the AWS SAM CLI on Windows<a name="serverless-sam-cli-install-windows"></a>

The following steps help you to install and configure the required prerequisites for using the AWS SAM CLI on your Windows host:

1. Create an AWS account\.

1. Configure IAM permissions\.

1. Install the AWS CLI\.

1. Create an Amazon S3 bucket\.

1. Install Docker\. Note: Docker is only a prerequisite for testing your application locally\.

1. Install the AWS SAM CLI\.

## Step 1: Create an AWS Account<a name="serverless-sam-cli-install-windows-aws-account"></a>

If you don't already have an AWS account, see [aws\.amazon\.com](https://aws.amazon.com/) and choose **Create an AWS Account**\. For detailed instructions, see [Create and Activate an AWS Account](https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)\.

## Step 2: Create an IAM User with Administrator Permissions<a name="serverless-sam-cli-install-windows-iam-permissions"></a>

If you don't already have an IAM user with administrator permissions, see [Creating Your First IAM Admin User and Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html) in the *IAM User Guide*\.

## Step 3: Install and Configure the AWS CLI<a name="serverless-sam-cli-install-windows-aws-cli"></a>

If you don't already have the AWS CLI installed, this step shows you how to install and configure it\. You can check whether you have the AWS CLI installed by executing `aws --version` at a command line\.

This section has two substeps: a\) Install the AWS CLI using an MSI installation package, and b\) Configure the AWS CLI to use your credentials, default AWS Region, and desired output format\.

### Step 3a: Install the AWS CLI<a name="serverless-sam-cli-install-windows-aws-cli-install"></a>

We recommend that you use one of the MSI installation packages\. These offer a familiar and convenient way to install the AWS CLI without installing any other prerequisites\.

Installing the AWS CLI using an MSI installation package is supported on Microsoft Windows XP or later\. For alternative installation options, see [Installing the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html)\.

**To install the AWS CLI using the MSI installer**

1. Download the appropriate MSI installer\.
   + [Download the AWS CLI MSI installer for Windows \(64\-bit\)](https://s3.amazonaws.com/aws-cli/AWSCLI64PY3.msi)\.
   + [Download the AWS CLI MSI installer for Windows \(32\-bit\)](https://s3.amazonaws.com/aws-cli/AWSCLI32PY3.msi)\.
   + [Download the AWS CLI setup file](https://s3.amazonaws.com/aws-cli/AWSCLISetup.exe) \(includes both the 32\-bit and 64\-bit MSI installers, and automatically installs the correct version\)\.

1. Run the downloaded MSI installer or the setup file\.

1. Follow the onscreen instructions\.

By default, the CLI installs to `C:\Program Files\Amazon\AWSCLI` \(64\-bit version\) or `C:\Program Files (x86)\Amazon\AWSCLI` \(32\-bit version\)\. To confirm the installation, use the `aws --version` command at a command line\.

### Step 3b: Configure the AWS CLI<a name="serverless-sam-cli-install-windows-aws-cli-configure"></a>

After you've verified installing the AWS CLI, you can configure it with your credentials, default AWS Region, and desired output format\. To do this, you first create the necessary access keys by following these steps:

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**\.

1. Choose the name of the user whose access keys you want to create, and then choose the **Security credentials** tab\.

1. In the **Access keys** section, choose **Create access key**\.

1. To view the new access key pair, choose **Show**\. You won't have access to the secret access key again after this dialog box closes\. Your credentials look something like this:
   + Access key ID: AKIAIOSFODNN7EXAMPLE
   + Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

1. To download the key pair, choose **Download \.csv file**\. Store the keys in a secure location\. You won't have access to the secret access key again after this dialog box closes\.

   Keep the keys confidential in order to protect your AWS account, and never email them\. Don't share them outside your organization, even if an inquiry appears to come from AWS or Amazon\.com\. No one who legitimately represents Amazon will ever ask you for your secret key\.

1. After you download the `.csv` file, choose **Close**\. When you create an access key, the key pair is active by default, and you can use the pair right away\.

Configure the AWS CLI with the access keys that you just created by executing the following command:

```
aws configure
```

When you're prompted, replace the following examples with your access keys:

```
 
 AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE                         # Enter your access key
 AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY # Enter your secret key
 Default region name [None]: us-east-1                                  # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
 Default output format [None]: json                                     # Or 'text'
```

Additional configuration options are available in [configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html)\.

## Step 4: Create an Amazon S3 Bucket<a name="serverless-sam-cli-install-windows-s3-bucket"></a>

AWS SAM uses an Amazon S3 bucket in your AWS account as a repository to store deployment artifacts\. To use the package and deployment functionality of AWS SAM, you must have an Amazon S3 bucket in the Region that you're working in\.

If you need to create an Amazon S3 bucket, you can run the following command:

```
aws s3 mb s3://bucketname --region region # Example regions: us-east-1, ap-east-1, eu-central-1, sa-east-1
```

You should see the following output for a successfully created Amazon S3 bucket:

```
 
 make_bucket: bucketname
```

Remember to keep track of your Amazon S3 bucket name because you need it to package your serverless application\.

## Step 5: Install Docker<a name="serverless-sam-cli-install-windows-docker"></a>

**Note**  
Docker is only a prerequisite for testing your application locally and building deployment packages using the `--use-container` flag\. You can skip this section or install Docker at a later time if you don't plan to use these features initially\.

Docker is an application that runs containers on your Linux machines\. AWS SAM provides a local environment that's similar to AWS Lambda to use as a Docker container\. You can use this container to build, test, and debug your serverless applications\.

You must have Docker installed and working to be able to run serverless projects and functions locally with the AWS SAM CLI\. The AWS SAM CLI uses the `DOCKER_HOST` environment variable to contact the Docker daemon\. The following steps describe how to install, configure, and verify a Docker installation to work with the AWS SAM CLI\.

1. Install Docker\.

   Docker Desktop supports the most recent Windows operating system\. For legacy versions of Windows, the Docker Toolbox is available\. Choose your version of Windows for the correct Docker installation steps:
   + To install Docker for Windows 10, see [Install Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)\.
   + To install Docker for older versions of Windows, see [Install Docker Toolbox on Windows](https://docs.docker.com/toolbox/toolbox_install_windows/)\.

1. Configure your shared drives\.

   The AWS SAM CLI requires that the project directory, or any parent directory, is listed in a shared drive\. Choose your version of Windows below for the correct shared drive instructions:
   + To share drives on Windows 10, see [ Docker Shared Drives](https://docs.docker.com/docker-for-windows/#shared-drives)\.
   + To share drives on older versions of Windows, see [Add Shared Directories](https://docs.docker.com/toolbox/toolbox_install_windows/#optional-add-shared-directories)\.

1. Verify the installation\.

   After Docker is installed, verify that it's working\. Also confirm that you can run Docker commands from the AWS SAM CLI \(for example, `docker ps`\)\. You don't need to install, fetch, or pull any containers—the AWS SAM CLI does this automatically as required\.

## Step 6: Install the AWS SAM CLI<a name="serverless-sam-cli-install-windows-sam-cli"></a>

Windows Installer \(MSI\) files are the package installer files for the Windows operating system\.

Follow these steps to install the AWS SAM CLI using the MSI file\. 

1. Install the AWS SAM CLI\.

   Choose your version of Windows for the correct MSI file:
   + [ 64\-bit](https://github.com/awslabs/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_64_PY3.msi)
   + [ 32\-bit](https://github.com/awslabs/aws-sam-cli/releases/latest/download/AWS_SAM_CLI_32_PY3.msi)

1. Verify the installation\.

   After completing the installation, verify it by opening a new command prompt or PowerShell prompt\. You should be able to invoke `sam` from the command line\.

   ```
   sam --version
   ```

   You should see output like the following after successful installation of the AWS SAM CLI:

   ```
    
    SAM CLI, version 0.17.0
   ```

You're now ready to start development\.

## Next Steps<a name="serverless-sam-cli-install-windows-next-steps"></a>

You're now ready to begin building your own serverless applications using AWS SAM\! If you want to start with sample serverless applications, choose one of the following links:
+ [Tutorial: Deploying a Hello World Application](serverless-getting-started-hello-world.md) – Step\-by\-step instructions to download, build, and deploy a simple serverless application\.
+ [AWS SAM example applications in GitHub](https://github.com/awslabs/serverless-application-model/tree/master/examples/apps) – Sample applications in the AWS SAM GitHub repository that you can further experiment with\.