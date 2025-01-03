# Configuring AWS s3

This section covers how to prepare your Amazon S3 storage to import data into the RedBrick AI platform. After following the instructions in this section, you will be able to create an Amazon S3 'storage method' on the RedBrick platform to connect your S3 bucket to your RedBrick account.

## Signing Up for AWS <a href="#signing-up-for-aws" id="signing-up-for-aws"></a>

The first step to preparing data storage on Amazon S3, is to sign up for an AWS account on [https://aws.amazon.com.](https://aws.amazon.com/)

## Create an S3 Bucket <a href="#create-an-s3-bucket" id="create-an-s3-bucket"></a>

{% hint style="info" %}
Skip creating a bucket if you want to use an existing bucket
{% endhint %}

Once you are logged in to your AWS account, head over to the Amazon S3 console.&#x20;

* Create a new bucket, give it a unique name (this will be needed later).
* Select the region of the bucket - we recommend keeping it close to your physical location for the best data transfer experience.
* We recommend **blocking all public access to your s3 bucket**, and giving the RedBrick AI interface access through IAM credentials. &#x20;
* You can leave all other settings as default. \
  \
  After creating your S3 bucket, **upload your images** through the User Interface, or use the AWS CLI for large amounts of data.

## S3 Bucket Settings <a href="#s3-bucket-settings" id="s3-bucket-settings"></a>

To ensure your data is private and secured, RedBrick uses pre-signed URL's to render data in browsers. To allow RedBrick to use pre-signed URL's to serve data, you need to define a CORS policy on the S3 bucket. [Here](https://docs.aws.amazon.com/AmazonS3/latest/dev/cors.html) is the AWS S3 documentation on CORS.

To set the proper CORS policy, go to the **Permissions tab** in your S3 bucket. Under Permissions select the CORS configuration and copy paste the following block of code.

```javascript
[
    {
        "AllowedHeaders": [
            "*"
        ],
        "AllowedMethods": [
            "PUT",
            "POST",
            "DELETE",
            "GET"
        ],
        "AllowedOrigins": [
            "*"
        ],
        "ExposeHeaders": [
            "x-amz-server-side-encryption",
            "x-amz-request-id",
            "x-amz-id-2"
        ],
        "MaxAgeSeconds": 3000
    }
]
```

![CORS Permissions on s3 bucket console](<../../.gitbook/assets/Screen Shot 2022-02-23 at 2.43.03 PM.png>)

## Access and Secret Keys <a href="#access-and-secret-keys" id="access-and-secret-keys"></a>

If your S3 Bucket blocks public access to the data, you will have to create an IAM user to allow RedBrick to securely access the data in your S3 bucket. AWS IAM enables you to manage access to your AWS services. You can read about IAM in the [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id\_users.html).

To create an IAM user from the AWS console, follow these steps:

1. Sign in to the AWS Management Console and open the IAM console
2. In the IAM console navigation pane, choose Users and then choose Add user.

#### Add User

1. Type the user name for the new user.
2. Select Programmatic Access

#### Permissions

* Click on Attach existing policies directly
* Create a new policy
* **Paste the following block of JSON inside the JSON tab**. Remember to replace `<your_s3_bucket_name_here>` with the name of the S3 bucket that has your data. You can modify the Resource path for added security or specificity.

```javascript
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "RedBrickLabelingReadOnly",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::<your_s3_bucket_name_here>/*"
    }
  ]
}
```

{% hint style="info" %}
If your bucket will be used as an annotation storage bucket, you need to add PUT object access as well.&#x20;
{% endhint %}

* Review your policy and create it.
* Head back to your IAM user creation and attach the policy you just created.

{% hint style="info" %}
**Granular Permissions**\
\
You can configure your S3 bucket to give RedBrick AI access to particular data points inside your s3 bucket by modifying the "Resource" section in the file above.&#x20;
{% endhint %}

#### Create the user

* Create the user and **download Access and Secret key .csv**
* Store the CSV file with your keys carefully.

## Items Path

Once you've created your AWS Storage method on RedBrick AI, you have to upload an items list to your projects to import specific datapoints. Please have a look at the [items list documentation](../import-cloud-data/creating-an-items-list.md) for a overview of the format for the JSON file.&#x20;

For data stored in an AWS s3 bucket, the `items` path needs to be formatted as follows:&#x20;

```json
"root-folder/sub-folder/datapoint.dcm"
```

Where `root-folder` is inside the AWS s3 bucket storage method.

## Programmatically Generate Items List For S3

If you don't have a standard naming convention for your files inside your s3 bucket, or you're not sure which files are in the s3 bucket, you can use the AWS CLI to enumerate a list of all the objects inside a bucket. Using this list, you can programmatically generate an items list.

### Installing and Configuring the AWS CLI <a href="#installing-and-configuring-the-aws-cli" id="installing-and-configuring-the-aws-cli"></a>

Have a look at the [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html) for installing the CLI. For mac users, running `brew install awscli` is the easiest way to install the AWS CLI.

Once you have the AWS CLI installed, you need to configure the cli with your AWS root account Access Key and Secret Key to give permissions to AWS CLI. After installing AWS CLI, do the following.

```bash
$ aws configure
AWS Access Key ID [None]: <your_access_key>
AWS Secret Access Key [None]: <your_secret_key>
Default region name [None]:
Default output format [None]:
```

After filling out your keys, you can leave the last two fields empty.

Now that your AWS CLI is configured, you can list out the objects inside your s3 bucket by running the following command.

```bash
$ aws s3 ls s3://<your_bucket_name>
```

After listing out all the images inside the s3 bucket (or a folder in the bucket), you can save the output to a txt file and write a simple script to convert that output into a JSON file in the format of the Items List covered above.
